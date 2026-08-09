---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "is и == в Python: в чём разница?"
subtitle: ""
summary: "Разбираемся, чем отличаются операторы is и == в Python, почему они могут возвращать разные результаты и в каких случаях использовать каждый из них."
authors: []
tags: [Python]
categories: [Python]
date: 2026-08-09T17:04:52+03:00
lastmod: 2026-08-09T17:04:52+03:00
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

<p align="justify">В Python для сравнения можно встретить как оператор `==`, так и `is`.</p>

<p align="justify">Рассмотрим простой пример:</p>

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

<p align="justify">Результат:</p>

```text
True
False
```

<p align="justify">Списки `a` и `b` содержат одинаковые значения, поэтому выражение `a == b` возвращает `True`. При этом сами списки были созданы отдельно. Это два разных объекта, поэтому `a is b` возвращает `False`.</p>

<p align="justify">Если изменить пример следующим образом:</p>

```python
a = [1, 2, 3]
b = a

print(a == b)
print(a is b)
```

<p align="justify">то результат будет уже другим:</p>

```text
True
True
```

<p align="justify">В данном случае новый список для `b` не создавался. Переменной `b` была присвоена ссылка на тот же объект, на который уже ссылается `a`.</p>

<p align="justify">Можно проверить это и с помощью функции `id()`:</p>

```python
a = [1, 2, 3]
b = a

print(id(a))
print(id(b))
```

<p align="justify">Значения `id` будут одинаковыми.</p>

<blockquote>
<p><code>==</code> отвечает на вопрос: «Одинаковые ли у объектов значения?»</p>
<p><code>is</code> отвечает на вопрос: «Это один и тот же объект?»</p>
</blockquote>

## Когда использовать `==`

<p align="justify">В большинстве обычных сравнений нужен именно оператор `==`.</p>

<p align="justify">Например:</p>

```python
age = 25

if age == 25:
    print("Возраст совпадает")
```

<p align="justify">То же самое относится к строкам:</p>

```python
name = "Ian"

if name == "Ian":
    print("Имя совпадает")
```

<p align="justify">И к коллекциям:</p>

```python
a = [1, 2, 3]
b = [1, 2, 3]

if a == b:
    print("Списки равны")
```

<p align="justify">Здесь нас интересует содержимое объектов, а не то, где именно они находятся в памяти.</p>

## Когда использовать `is`

<p align="justify">`is` имеет смысл в тех случаях, когда необходимо проверить идентичность объекта.</p>

<p align="justify">Наиболее распространённый пример — `None`:</p>

```python
result = None

if result is None:
    print("Результата нет")
```

<p align="justify">Для обратной проверки используется `is not`:</p>

```python
if result is not None:
    print(result)
```

<p align="justify">Именно такой вариант обычно используется в Python-коде вместо:</p>

```python
if result == None:
    ...
```

## Почему `is` иногда работает с числами и строками

<p align="justify">Иногда можно встретить такой код:</p>

```python
a = 10
b = 10

print(a is b)
```

<p align="justify">И получить:</p>

```text
True
```

<p align="justify">После этого может показаться, что `is` вполне подходит для сравнения чисел.</p>

<p align="justify">Однако полагаться на такое поведение не нужно. Python может повторно использовать некоторые уже созданные объекты. Это относится, например, к некоторым целым числам и строкам.</p>

<p align="justify">Поэтому писать:</p>

```python
if number is 10:
    ...
```

<p align="justify">неправильно.</p>

<p align="justify">Нужно использовать:</p>

```python
if number == 10:
    ...
```

<p align="justify">То же относится и к строкам:</p>

```python
if status == "active":
    ...
```

<p align="justify">а не:</p>

```python
if status is "active":
    ...
```

<p align="justify">Работа программы не должна зависеть от того, использовал Python существующий объект повторно или создал новый.</p>
