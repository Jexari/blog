---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Python-фичи, которые стоит знать"
subtitle: ""
summary: "Разбираем mutable default arguments, *args, **kwargs, области видимости LEGB, lambda-функции и type hints на простых примерах."
authors: [admin]
tags: [Python]
categories: [Python]
date: 2026-08-10T17:58:27+03:00
lastmod: 2026-08-10T17:58:27+03:00
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

<details class="toc-inpage d-print-none  " open="">
<summary class="font-weight-bold">Содержание</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#introduction" class="nav-link"><span class="section-num">1</span> Введение</a></li>
<li class="nav-item"><a href="#mutable-default-arguments" class="nav-link"><span class="section-num">2</span> Mutable default arguments </a></li>
<li class="nav-item"><a href="#args" class="nav-link"><span class="section-num">3</span> *args </a></li>
<li class="nav-item"><a href="#kwargs" class="nav-link"><span class="section-num">4</span> **kwargs </a></li>
<li class="nav-item"><a href="#legb" class="nav-link"><span class="section-num">5</span> Scope и правило LEGB </a></li>
<li class="nav-item"><a href="#lambda" class="nav-link"><span class="section-num">6</span> Lambda-функции </a></li>
<li class="nav-item"><a href="#type-hints" class="nav-link"><span class="section-num">7</span> Type hints </a></li>
<li class="nav-item"><a href="#conclusion" class="nav-link"><span class="section-num">8</span> Заключение </a></li>
</ul>
</nav>
</details>

<h2 id="introduction">1. Введение</h2>

<p align="justify" >Когда только начинаешь изучать Python, функции выглядят довольно просто: передал несколько аргументов, получил результат. Но постепенно появляются значения по умолчанию, произвольное количество параметров, вложенные функции и аннотации типов. В этот момент становится понятно, что с функциями в Python связано гораздо больше механик, чем кажется на первый взгляд.</p>

<p align="justify" >Большая часть вещей из этой статьи не относится к каким-то редким трюкам языка. Наоборот, их можно встретить практически в любом достаточно крупном Python-проекте. Поэтому полезно понимать не только синтаксис, но и то, что происходит за ним.</p>

<h2 id="mutable-default-arguments">2. Mutable default arguments</h2>

<p align="justify" >Начнем с одной из самых известных особенностей Python — изменяемых объектов в аргументах функции по умолчанию.</p>

<p align="justify" >Представим, что нам нужна функция, которая добавляет переданное значение в список. На первый взгляд следующий код выглядит вполне логично:</p>

```python
def add_item(item, items=[]):
    items.append(item)
    return items


print(add_item("Python"))
print(add_item("Java"))
```

<p align="justify" >Можно ожидать, что результат будет примерно таким:</p>

```text
['Python']
['Java']
```

<p align="justify" >Но на самом деле получится:</p>

```text
['Python']
['Python', 'Java']
```

<p align="justify" >Причина в том, что значение аргумента по умолчанию создается не при каждом вызове функции. Оно создается один раз — в момент определения самой функции. После этого следующие вызовы продолжают работать с тем же объектом.</p>

<p align="justify" >Список является <em>mutable</em>, то есть изменяемым объектом. Когда мы вызываем <em>append()</em>, изменяется уже существующий список, и это изменение сохраняется для следующего вызова функции.</p>

<p align="justify" >Обычно такую функцию лучше написать через <em>None</em>:</p>

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items


print(add_item("Python"))
print(add_item("Java"))
```

<p align="justify" >Теперь при каждом вызове без второго аргумента внутри функции создается новый список:</p>

```text
['Python']
['Java']
```

<p align="justify" >То же самое касается словарей, множеств и других изменяемых объектов. Например, конструкция <em>config={}</em> в параметрах функции может привести к точно такому же поведению.</p>

<p align="justify" >При этом само поведение Python иногда можно использовать специально. Например, таким способом можно хранить некоторое состояние между вызовами функции. Но такой код обычно не самый очевидный для человека, который будет читать его позже, поэтому для хранения состояния лучше использовать более явные решения.</p>

<h2 id="args">3. *args</h2>

<p align="justify" >Обычно количество аргументов функции известно заранее:</p>

```python
def add(a, b):
    return a + b
```

<p align="justify" >Но иногда заранее неизвестно, сколько значений будет передано. Для этого в Python существует конструкция <em>*args</em>.</p>

```python
def add(*args):
    print(args)


add(1, 2, 3, 4)
```

<p align="justify" >В результате получим:</p>

```text
(1, 2, 3, 4)
```

<p align="justify" ><em>args</em> внутри функции является обычным кортежем. Поэтому с ним можно работать так же, как с любым другим <em>tuple</em>.</p>

<p align="justify" >Например, можно написать функцию, которая складывает любое количество чисел:</p>

```python
def add(*args):
    result = 0

    for number in args:
        result += number

    return result


print(add(1, 2))
print(add(1, 2, 3, 4, 5))
```

<p align="justify" >Название <em>args</em> само по себе не является специальным словом Python. Важна именно звездочка перед названием параметра.</p>

<p align="justify" >Технически функцию можно написать и так:</p>

```python
def add(*numbers):
    return sum(numbers)
```

<p align="justify" >Однако вариант <em>*args</em> стал стандартным соглашением и хорошо знаком большинству Python-разработчиков.</p>

<p align="justify" >Звездочка используется не только при объявлении функции. С ее помощью можно также распаковать последовательность при вызове.</p>

```python
def print_user(name, age):
    print(name, age)


user = ["Alex", 25]

print_user(*user)
```

<p align="justify" >Этот вызов фактически будет эквивалентен следующему:</p>

```python
print_user("Alex", 25)
```

<p align="justify" >Такую распаковку удобно использовать, когда аргументы уже находятся внутри списка или кортежа.</p>

<h2 id="kwargs">4. **kwargs</h2>

<p align="justify" >Если <em>*args</em> позволяет принимать произвольное количество позиционных аргументов, то <em>**kwargs</em> делает похожую вещь с именованными аргументами.</p>

```python
def show_user(**kwargs):
    print(kwargs)


show_user(name="Alex", age=25, city="Madrid")
```

<p align="justify" >Внутри функции получим обычный словарь:</p>

```text
{'name': 'Alex', 'age': 25, 'city': 'Madrid'}
```

<p align="justify" >Поэтому значения можно получать привычным способом:</p>

```python
def show_user(**kwargs):
    print(kwargs.get("name"))
    print(kwargs.get("age"))


show_user(name="Alex", age=25)
```

<p align="justify" >Как и в случае с <em>args</em>, название <em>kwargs</em> является соглашением, а не обязательной частью синтаксиса. Важны две звездочки.</p>

<p align="justify" ><em>*args</em> и <em>**kwargs</em> часто используются вместе:</p>

```python
def example(*args, **kwargs):
    print("args:", args)
    print("kwargs:", kwargs)


example(1, 2, 3, language="Python", version=3)
```

<p align="justify" >Получим:</p>

```text
args: (1, 2, 3)
kwargs: {'language': 'Python', 'version': 3}
```

<p align="justify" >Через две звездочки можно также распаковывать словари при вызове функции.</p>

```python
def create_user(name, age):
    print(f"{name}: {age}")


user = {
    "name": "Alex",
    "age": 25
}

create_user(**user)
```

<p align="justify" >Python возьмет ключи словаря как имена аргументов, а соответствующие значения — как значения этих аргументов.</p>

<p align="justify" >Такая возможность особенно полезна при работе с конфигурациями, декораторами, библиотеками и функциями-обертками, когда заранее неизвестно, какие именно параметры придется передавать дальше.</p>

<h2 id="legb">5. Scope и правило LEGB</h2>

<p align="justify" >Еще одна важная тема в Python — области видимости переменных, или <em>scope</em>. Если в программе существует несколько переменных с одинаковым названием, интерпретатору нужно определить, какую именно из них использовать.</p>

<p align="justify" >Для этого обычно используют правило <em>LEGB</em>:</p>

<ul>
<li><em>L — Local</em></li>
<li><em>E — Enclosing</em></li>
<li><em>G — Global</em></li>
<li><em>B — Built-in</em></li>
</ul>

<p align="justify" >Python ищет имя именно в таком порядке.</p>

<h3>Local</h3>

<p align="justify" ><em>Local</em> — локальная область текущей функции.</p>

```python
def example():
    language = "Python"
    print(language)


example()
```

<p align="justify" >Переменная <em>language</em> существует внутри функции. Если попробовать обратиться к ней снаружи, Python ее не найдет.</p>

<h3>Enclosing</h3>

<p align="justify" ><em>Enclosing</em> появляется, когда одна функция находится внутри другой.</p>

```python
def outer():
    language = "Python"

    def inner():
        print(language)

    inner()


outer()
```

<p align="justify" >В функции <em>inner()</em> переменной <em>language</em> нет. Поэтому Python переходит на следующий уровень и ищет ее в области функции <em>outer()</em>.</p>

<p align="justify" >Если нам нужно не просто прочитать такую переменную, а изменить ее, используется ключевое слово <em>nonlocal</em>.</p>

```python
def counter():
    value = 0

    def increment():
        nonlocal value
        value += 1
        return value

    print(increment())
    print(increment())


counter()
```

<p align="justify" >Здесь <em>nonlocal</em> сообщает Python, что нужно использовать переменную из внешней функции, а не создавать новую локальную.</p>

<h3>Global</h3>

<p align="justify" ><em>Global</em> — уровень текущего модуля.</p>

```python
language = "Python"


def show_language():
    print(language)


show_language()
```

<p align="justify" >Функция не находит <em>language</em> локально и во внешней функции, поэтому доходит до глобальной области.</p>

<p align="justify" >Чтобы изменить глобальную переменную внутри функции, существует ключевое слово <em>global</em>:</p>

```python
counter = 0


def increment():
    global counter
    counter += 1


increment()
print(counter)
```

<p align="justify" >После вызова значение <em>counter</em> будет равно <em>1</em>.</p>

<p align="justify" >При этом злоупотреблять глобальными переменными обычно не стоит. Когда разные функции напрямую изменяют общее глобальное состояние, становится сложнее понимать, откуда именно взялось текущее значение.</p>

<h3>Built-in</h3>

<p align="justify" >Последний уровень — <em>Built-in</em>. Здесь находятся встроенные имена Python: например, <em>print</em>, <em>len</em>, <em>sum</em>, <em>str</em> и многие другие.</p>

```python
numbers = [1, 2, 3]

print(len(numbers))
```

<p align="justify" >Если создать собственную переменную с таким же именем, можно случайно перекрыть встроенную функцию:</p>

```python
len = 10

numbers = [1, 2, 3]

print(len(numbers))
```

<p align="justify" >Теперь <em>len</em> содержит число, а не встроенную функцию, поэтому попытка вызвать его закончится ошибкой.</p>

<p align="justify" >В итоге правило можно запомнить довольно просто: <em>Local → Enclosing → Global → Built-in</em>. Python идет от самой близкой области видимости к самой общей и останавливается, как только находит нужное имя.</p>

<h2 id="lambda">6. Lambda-функции</h2>

<p align="justify" ><em>Lambda</em> позволяет создавать небольшие функции без обычного объявления через <em>def</em>.</p>

<p align="justify" >Например, обычная функция:</p>

```python
def square(number):
    return number ** 2
```

<p align="justify" >С помощью <em>lambda</em> ее можно записать так:</p>

```python
square = lambda number: number ** 2

print(square(5))
```

<p align="justify" >Результат в обоих случаях будет одинаковым:</p>

```text
25
```

<p align="justify" >Общий синтаксис выглядит следующим образом:</p>

```python
lambda arguments: expression
```

<p align="justify" >Главное ограничение состоит в том, что после двоеточия находится одно выражение. Поэтому <em>lambda</em> подходит именно для небольших операций, а не для полноценной функции на десять строк.</p>

<p align="justify" >Особенно удобно использовать ее там, где функция нужна только один раз. Например, при сортировке:</p>

```python
users = [
    {"name": "Alex", "age": 27},
    {"name": "Max", "age": 21},
    {"name": "Kate", "age": 24},
]

users.sort(key=lambda user: user["age"])

print(users)
```

<p align="justify" >Здесь функция нужна только для того, чтобы сообщить методу <em>sort()</em>, по какому значению сортировать элементы.</p>

<p align="justify" >Еще один распространенный пример — использование вместе с <em>map()</em> или <em>filter()</em>:</p>

```python
numbers = [1, 2, 3, 4, 5]

squares = list(map(lambda number: number ** 2, numbers))

print(squares)
```

<p align="justify" >Результат:</p>

```text
[1, 4, 9, 16, 25]
```

<p align="justify" >Но сокращать код любой ценой не стоит. Если <em>lambda</em> становится слишком длинной или внутри появляется сложная логика, обычная функция через <em>def</em> почти всегда будет читаться лучше.</p>

<h2 id="type-hints">7. Type hints</h2>

<p align="justify" >Python относится к языкам с динамической типизацией. Нам не нужно заранее объявлять тип каждой переменной, и одна и та же переменная в разное время может ссылаться на объекты разных типов.</p>

```python
value = 10
value = "Python"
```

<p align="justify" >Это удобно, но в больших проектах иногда становится сложно понять, какие данные функция ожидает получить и что она должна вернуть. Для этого используются <em>type hints</em> — аннотации типов.</p>

<p align="justify" >Например, обычная функция может выглядеть так:</p>

```python
def greet(name):
    return f"Hello, {name}"
```

<p align="justify" >Добавим информацию о типах:</p>

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

<p align="justify" >Теперь из объявления функции сразу понятно, что аргумент <em>name</em> ожидается как строка и функция должна возвращать строку.</p>

<p align="justify" >При этом Python сам по себе обычно не запрещает передать значение другого типа только из-за аннотации.</p>

```python
def greet(name: str) -> str:
    return f"Hello, {name}"


print(greet(123))
```

<p align="justify" >Аннотации в первую очередь дают дополнительную информацию разработчику и инструментам анализа кода. IDE и статические анализаторы могут заметить несоответствие типов еще до запуска программы.</p>

<p align="justify" >Типизировать можно и коллекции:</p>

```python
def get_names(users: list[str]) -> list[str]:
    return [user.upper() for user in users]
```

<p align="justify" >Если значение может иметь несколько типов, в современных версиях Python можно использовать оператор <em>|</em>:</p>

```python
def find_user(user_id: int) -> str | None:
    if user_id == 1:
        return "Alex"

    return None
```

<p align="justify" >Запись <em>str | None</em> показывает, что функция может вернуть либо строку, либо <em>None</em>.</p>

<p align="justify" >Для более сложных случаев существует модуль <em>typing</em>. Например, с помощью <em>Callable</em> можно описывать функции, передаваемые как аргументы.</p>

```python
from typing import Callable


def calculate(
    a: int,
    b: int,
    operation: Callable[[int, int], int]
) -> int:
    return operation(a, b)


result = calculate(10, 5, lambda a, b: a + b)

print(result)
```

<p align="justify" >Type hints особенно полезны не потому, что делают Python похожим на строго типизированные языки, а потому, что выступают своеобразной документацией прямо внутри кода. Когда функция имеет пять аргументов и возвращает сложную структуру, аннотации сильно упрощают ее чтение.</p>

<h2 id="conclusion">8. Заключение</h2>

<p align="justify" >На первый взгляд рассмотренные возможности почти никак не связаны между собой. <em>*args</em> и <em>**kwargs</em> отвечают за передачу аргументов, <em>LEGB</em> — за поиск имен, <em>lambda</em> — за создание небольших функций, а <em>type hints</em> помогают описывать ожидаемые типы данных.</p>

<p align="justify" >Но все эти механики объединяет одна вещь: они постоянно встречаются в обычном Python-коде. Без понимания <em>mutable default arguments</em> легко получить неожиданное состояние между вызовами функции. Без <em>*args</em> и <em>**kwargs</em> сложнее писать универсальные функции и обертки. А понимание областей видимости помогает разобраться, откуда Python вообще берет значение переменной.</p>

<p align="justify" ><em>Lambda</em> и <em>type hints</em> скорее относятся к удобству написания и чтения программы. Первая позволяет компактно описывать небольшие операции, а вторые делают интерфейс функций значительно понятнее.</p>

<p align="justify" >Это далеко не все особенности Python, которые стоит знать. У языка есть декораторы, генераторы, контекстные менеджеры, comprehensions, распаковка, <em>property</em>, <em>dataclasses</em> и множество других интересных механизмов. Но это уже темы для отдельного продолжения.</p>

