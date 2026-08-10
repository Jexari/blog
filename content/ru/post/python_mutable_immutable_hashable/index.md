---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Mutable, immutable и при чём здесь hashable"
subtitle: ""
summary: "Разбираемся, чем mutable-объекты отличаются от immutable, что означает hashable в Python, почему список нельзя использовать как ключ словаря и почему immutable не всегда означает hashable."
authors: [admin]
tags: [Python]
categories: [Python]
date: 2026-08-10T00:45:26+03:00
lastmod: 2026-08-10T00:45:26+03:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

<p align="justify">В Python довольно часто рядом встречаются понятия mutable, immutable, hashable и unhashable. Особенно когда речь заходит про списки, кортежи, словари и множества. Поначалу между ними легко провести слишком простую связь: изменяемые объекты нельзя хешировать, неизменяемые — можно.</p>

<p align="justify">В большинстве повседневных примеров это действительно похоже на правду. Список изменяемый и unhashable, строка неизменяемая и hashable. Но если копнуть немного глубже, выясняется, что это всё-таки разные свойства объекта.</p>

<p align="justify">Начнём с mutable и immutable.</p>

<p align="justify">Mutable — это объект, который можно изменить после его создания. Самый очевидный пример — обычный список:</p>

```python id="0bjfh6"
numbers = [1, 2, 3]
numbers.append(4)

print(numbers)
# [1, 2, 3, 4]
```

<p align="justify">Здесь список, который изначально содержал три элемента, стал содержать четыре. Причём это всё ещё тот же самый объект.</p>

<p align="justify">Можно даже посмотреть на его <em>id</em>:</p>

```python id="ttrm6v"
numbers = [1, 2, 3]

print(id(numbers))

numbers.append(4)

print(id(numbers))
```

<p align="justify">В обоих случаях <em>id</em> будет одинаковым. Мы взяли существующий объект и изменили его.</p>

<p align="justify">Со строками всё работает иначе. Строки в Python immutable, то есть после создания изменить сам объект уже нельзя.</p>

<p align="justify">Например, сделать так не получится:</p>

```python id="f6lvd5"
name = "cat"
name[0] = "b"
```

<p align="justify">Python выдаст <em>TypeError</em>.</p>

<p align="justify">При этом никто не запрещает написать:</p>

```python id="imfsr1"
name = "cat"
name = "bat"
```

<p align="justify">На первый взгляд кажется, что мы всё-таки изменили строку. Но нет. Переменная `name` раньше ссылалась на строку <em>"cat"</em>, а после второго присваивания стала ссылаться на другой объект — строку <em>"bat"</em>.</p>

<p align="justify">Это довольно важный момент. Immutable не означает, что переменную нельзя поменять. Переменная вообще не является самим объектом. Грубо говоря, это имя, которое на него ссылается. Поменять можно ссылку, но не сам immutable-объект.</p>

<p align="justify">То же самое происходит с числами:</p>

```python id="j5n8t8"
x = 10
x += 1
```

<p align="justify">Число <em>10</em> не превратилось в <em>11</em>. В результате операции `x` просто стал ссылаться на другое значение.</p>

<p align="justify">К изменяемым встроенным типам относятся, например, <em>list</em>, <em>dict</em> и <em>set</em>. К неизменяемым — <em>int</em>, <em>float</em>, <em>bool</em>, <em>str</em>, <em>bytes</em>, <em>tuple</em> и <em>frozenset</em>.</p>

<p align="justify">И вот где-то здесь обычно появляется второй вопрос: почему список нельзя использовать как ключ словаря, а кортеж можно?</p>

```python id="e1zq46"
data = {
    (10, 20): "point"
}
```

<p align="justify">Такой словарь совершенно нормален.</p>

<p align="justify">А вот такой:</p>

```python id="x6m04w"
data = {
    [10, 20]: "point"
}
```

<p align="justify">даже не создастся:</p>

```text id="i1h71n"
TypeError: unhashable type: 'list'
```

<p align="justify">Чтобы понять причину, нужно разобраться с hashable.</p>

<p align="justify">У Python есть встроенная функция <em>hash()</em>:</p>

```python id="pdeftw"
hash(42)
hash("hello")
hash((1, 2, 3))
```

<p align="justify">Все эти вызовы работают и возвращают некоторое целое число. Само число обычно нас вообще не интересует. Важно то, что Python может получить для объекта hash и использовать его в хеш-таблицах, на которых построены, в частности, словари и множества.</p>

<p align="justify">Например, когда мы пишем:</p>

```python id="1nm6v1"
users = {
    "alice": 25,
    "bob": 31,
}
```

<p align="justify">Python не перебирает каждый ключ словаря с начала до конца каждый раз, когда мы обращаемся к <em>users["alice"]</em>. Hash ключа помогает быстро определить, где искать нужную запись.</p>

<p align="justify">Отсюда возникает важное требование: hash объекта должен оставаться стабильным, пока объект используется таким образом.</p>

<p align="justify">И тут становится понятно, почему список создаёт проблему.</p>

<p align="justify">Представим на секунду, что Python разрешал бы такое:</p>

```python id="4fnf9e"
key = [1, 2]

data = {
    key: "hello"
}
```

<p align="justify">Python вычислил бы hash <em>[1, 2]</em> и на его основе положил запись в определённое место внутри словаря.</p>

<p align="justify">А потом мы сделали бы:</p>

```python id="4a70y6"
key.append(3)
```

<p align="justify">Теперь наш ключ уже <em>[1, 2, 3]</em>.</p>

<p align="justify">Если hash зависит от содержимого списка, он тоже должен измениться. Получается странная ситуация: запись была положена в словарь с одним hash, а искать её теперь пришлось бы с другим.</p>

<p align="justify">Поэтому обычный <em>list</em> просто нельзя хешировать:</p>

```python id="8fhf4d"
hash([1, 2, 3])
```

<p align="justify">закончится ошибкой:</p>

```text id="hqm6bj"
TypeError: unhashable type: 'list'
```

<p align="justify">То же самое происходит с <em>dict</em> и <em>set</em>. Все они изменяемые и поэтому не подходят для обычного хеширования по своему содержимому.</p>

<p align="justify">Именно отсюда и берётся удобная ассоциация:</p>

```text id="n2fnlw"
list  → mutable   → unhashable
dict  → mutable   → unhashable
set   → mutable   → unhashable

str   → immutable → hashable
int   → immutable → hashable
bytes → immutable → hashable
```

<p align="justify">Но воспринимать это как строгое правило всё-таки не стоит.</p>

<p align="justify">Хороший пример — <em>tuple</em>.</p>

<p align="justify">Кортеж изменить нельзя:</p>

```python id="z0a5fx"
point = (10, 20)
point[0] = 100
```

<p align="justify">Получим ошибку. Поэтому вполне логично ожидать, что кортеж можно хешировать:</p>

```python id="57vexd"
point = (10, 20)

print(hash(point))
```

<p align="justify">И действительно можно.</p>

<p align="justify">Благодаря этому кортежи удобно использовать как ключи словарей. Например, координаты:</p>

```python id="8bc4gk"
places = {
    (40.7128, -74.0060): "New York",
    (51.5074, -0.1278): "London",
}
```

<p align="justify">Но теперь положим внутрь кортежа список:</p>

```python id="eek3if"
value = (1, 2, [3, 4])
```

<p align="justify">Сам кортеж всё ещё immutable. Нельзя написать:</p>

```python id="mvkd87"
value[0] = 100
```

<p align="justify">Но список внутри него никто не запрещает менять:</p>

```python id="k8rgl7"
value[2].append(5)

print(value)
# (1, 2, [3, 4, 5])
```

<p align="justify">А теперь попробуем:</p>

```python id="71ayfn"
hash(value)
```

<p align="justify">и получим <em>TypeError</em>.</p>

<p align="justify">То есть <em>tuple</em> сам по себе immutable, но это ещё не гарантирует, что конкретный кортеж будет hashable. Его элементы тоже должны быть hashable.</p>

<p align="justify">С этим связан забавный момент: фраза «кортеж нельзя изменить» иногда воспринимается слишком буквально. Нельзя изменить то, на какие объекты ссылаются позиции кортежа. Но если внутри кортежа лежит mutable-объект, например список, сам этот объект вполне можно изменить.</p>

<p align="justify">Похожая история есть у множеств. Обычный <em>set</em> можно менять:</p>

```python id="pdk8j5"
numbers = {1, 2, 3}
numbers.add(4)
```

<p align="justify">Поэтому сам <em>set</em> unhashable и не может быть элементом другого множества.</p>

<p align="justify">Но в Python существует <em>frozenset</em>:</p>

```python id="th8j9z"
numbers = frozenset({1, 2, 3})

print(hash(numbers))
```

<p align="justify">Это уже неизменяемое множество, и его можно хешировать. Поэтому <em>frozenset</em>, в отличие от обычного <em>set</em>, может быть ключом словаря или элементом другого множества.</p>

<p align="justify">Есть ещё одно правило, которое хорошо объясняет смысл hashability. Если два hashable-объекта равны:</p>

```python id="8f6klx"
a == b
```

<p align="justify">то их hash тоже обязан быть одинаковым:</p>

```python id="kvrtll"
hash(a) == hash(b)
```

<p align="justify">То есть из <em>a == b</em> должно следовать равенство хешей.</p>

<p align="justify">А вот наоборот это не работает. Два разных объекта теоретически могут получить одинаковый hash. Это называется коллизией, и Python умеет с такими ситуациями работать.</p>

<p align="justify">На практике всё это становится гораздо проще, если не пытаться объединить mutable и hashable в одно понятие.</p>

<p align="justify">Mutable и immutable говорят о том, можно ли изменить состояние объекта после его создания.</p>

<p align="justify">Hashable и unhashable говорят о том, подходит ли объект для использования в хеш-структурах Python. В первую очередь это означает возможность быть ключом <em>dict</em> или элементом <em>set</em>.</p>

<p align="justify">Для стандартных типов отсюда получается довольно знакомая картина. Строки, числа и подходящие кортежи можно использовать как ключи словаря. Списки, словари и множества — нельзя.</p>

```python id="4th8u2"
data = {
    "name": "Alice",       # str — можно
    42: "answer",          # int — можно
    (10, 20): "point",     # tuple — можно
}
```

<p align="justify">А вот:</p>

```python id="ppzfcq"
data = {
    [10, 20]: "point"
}
```

<p align="justify">не сработает.</p>

<p align="justify">И, пожалуй, это тот случай, когда понимание причины полезнее, чем заучивание таблицы типов. Если помнить, зачем словарю вообще нужен hash и почему этот hash должен оставаться стабильным, поведение <em>list</em>, <em>tuple</em>, <em>set</em> и <em>frozenset</em> перестаёт выглядеть набором случайных правил.</p>
