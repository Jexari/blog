---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Python: enumerate() и zip()"
subtitle: ""
summary: "Разбираемся, как работают enumerate() и zip() в Python, когда они удобнее ручной работы с индексами и как использовать их вместе."
authors: [admin]
tags: [Python]
categories: [Python]
date: 2026-08-10T00:45:54+03:00
lastmod: 2026-08-10T00:45:54+03:00
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

<p align="justify">Есть две функции, после знакомства с которыми часть циклов в Python начинает выглядеть заметно приятнее — <em>enumerate()</em> и <em>zip()</em>.</p>

<p align="justify">Обе довольно простые, поэтому тут лучше сразу идти к примерам.</p>

<p align="justify"><strong>enumerate()</strong></p>

<p align="justify">Допустим, есть список языков:</p>

```python
languages = ["Python", "Go", "Rust"]
```

<p align="justify">Хотим вывести не только название, но и его номер.</p>

<p align="justify">Можно сделать так:</p>

```python
for i in range(len(languages)):
    print(i, languages[i])
```

<p align="justify">Работает, но выглядит немного как обходной путь. Мы получаем длину списка, строим <em>range()</em>, затем используем индекс, чтобы снова обратиться к списку.</p>

<p align="justify">В Python для этого есть <em>enumerate()</em>:</p>

```python
for i, language in enumerate(languages):
    print(i, language)
```

<p align="justify">Результат:</p>

```text
0 Python
1 Go
2 Rust
```

<p align="justify">По сути, <em>enumerate()</em> во время обхода добавляет к каждому элементу счётчик.</p>

```python
list(enumerate(languages))
```

```text
[
    (0, "Python"),
    (1, "Go"),
    (2, "Rust"),
]
```

<p align="justify">А запись:</p>

```python
for i, language in enumerate(languages):
```

<p align="justify">просто распаковывает эти пары в две переменные.</p>

<p align="justify">Часто нумерация с нуля нам вообще не нужна. Например, если выводим рейтинг:</p>

```python
languages = ["Python", "Go", "Rust"]

for position, language in enumerate(languages, start=1):
    print(f"{position}. {language}")
```

<p align="justify">Получится:</p>

```text
1. Python
2. Go
3. Rust
```

<p align="justify">Мне кажется, это один из тех случаев, где код практически читается как обычный текст.</p>

<p align="justify">Кстати, число от <em>enumerate()</em> правильнее называть счётчиком, а не индексом. При обычном <em>enumerate(languages)</em> оно совпадает с индексом списка, но никто не мешает написать:</p>

```python
enumerate(languages, start=42)
```

<p align="justify">Сам список от этого, конечно, не начнёт индексироваться с 42.</p>

<p align="justify"><strong>zip()</strong></p>

<p align="justify">Теперь другая частая ситуация.</p>

<p align="justify">Есть имена:</p>

```python
names = ["Alice", "Bob", "Charlie"]
```

<p align="justify">И отдельно возраст:</p>

```python
ages = [25, 31, 28]
```

<p align="justify">Нужно пройти по ним одновременно.</p>

<p align="justify">Опять же, можно использовать индексы:</p>

```python
for i in range(len(names)):
    print(names[i], ages[i])
```

<p align="justify">Но проще:</p>

```python
for name, age in zip(names, ages):
    print(name, age)
```

<p align="justify">Получим:</p>

```text
Alice 25
Bob 31
Charlie 28
```

<p align="justify">Название <em>zip()</em> здесь довольно удачное. Функция как будто застёгивает две последовательности вместе.</p>

```text
Alice    25
Bob      31
Charlie  28
```

<p align="justify">Если посмотреть на результат через <em>list()</em>:</p>

```python
list(zip(names, ages))
```

<p align="justify">получим:</p>

```text
[
    ("Alice", 25),
    ("Bob", 31),
    ("Charlie", 28),
]
```

<p align="justify">Причём последовательностей может быть сколько угодно:</p>

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 31, 28]
cities = ["London", "Berlin", "Madrid"]

for name, age, city in zip(names, ages, cities):
    print(name, age, city)
```

<p align="justify">Никакой работы с индексами здесь уже не требуется.</p>

<p align="justify"><strong>Есть один нюанс с zip()</strong></p>

<p align="justify">Что произойдёт, если списки разной длины?</p>

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 31]

for name, age in zip(names, ages):
    print(name, age)
```

<p align="justify">Результат:</p>

```text
Alice 25
Bob 31
```

<p align="justify">Charlie просто не попадёт в цикл.</p>

<p align="justify"><em>zip()</em> заканчивает работу вместе с самой короткой последовательностью.</p>

<p align="justify">Иногда именно это и нужно. А иногда это баг, который хотелось бы заметить.</p>

<p align="justify">Если длины обязаны совпадать, можно написать:</p>

```python
for name, age in zip(names, ages, strict=True):
    print(name, age)
```

<p align="justify">Тогда при несовпадении длин получим <em>ValueError</em>.</p>

<p align="justify"><strong>Из zip() удобно делать словари</strong></p>

<p align="justify">Есть список полей:</p>

```python
fields = ["name", "age", "city"]
```

<p align="justify">И список значений:</p>

```python
values = ["Alice", 25, "London"]
```

<p align="justify">Можно соединить их:</p>

```python
user = dict(zip(fields, values))
```

<p align="justify">И получить:</p>

```python
{
    "name": "Alice",
    "age": 25,
    "city": "London",
}
```

<p align="justify">Простой приём, но периодически оказывается очень кстати.</p>

<p align="justify"><strong>А можно использовать их вместе</strong></p>

<p align="justify">Допустим, у нас есть участники и их результаты:</p>

```python
names = ["Alice", "Bob", "Charlie"]
scores = [95, 87, 91]
```

<p align="justify">Хотим вывести:</p>

```text
1. Alice — 95
2. Bob — 87
3. Charlie — 91
```

<p align="justify">Тогда можно совместить обе функции:</p>

```python
for position, (name, score) in enumerate(
    zip(names, scores),
    start=1,
):
    print(f"{position}. {name} — {score}")
```

<p align="justify">На первый взгляд эта конструкция может выглядеть немного странно:</p>

```python
position, (name, score)
```

<p align="justify">Но если посмотреть на данные, всё становится понятнее.</p>

<p align="justify"><em>zip()</em> даёт:</p>

```text
("Alice", 95)
("Bob", 87)
("Charlie", 91)
```

<p align="justify">А <em>enumerate()</em> добавляет к каждой такой паре номер:</p>

```text
(1, ("Alice", 95))
(2, ("Bob", 87))
(3, ("Charlie", 91))
```

<p align="justify">Отсюда и такая распаковка:</p>

```python
position, (name, score)
```

<p align="justify">Главная идея здесь та же, что и во многих других возможностях Python: если приходится вручную управлять индексами, стоит сначала проверить, нет ли способа выразить задачу напрямую.</p>
