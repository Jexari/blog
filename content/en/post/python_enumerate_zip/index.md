---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Python: enumerate() and zip()"
subtitle: ""
summary: "A look at how enumerate() and zip() work in Python, when they are more convenient than working with indices manually, and how to use them together."
authors: []
tags: []
categories: []
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

<p align="justify">There are two functions that, once you get familiar with them, make some loops in Python look noticeably cleaner — <em>enumerate()</em> and <em>zip()</em>.</p>

<p align="justify">Both are quite simple, so it's better to jump straight into examples.</p>

<p align="justify"><strong>enumerate()</strong></p>

<p align="justify">Suppose we have a list of languages:</p>

```python
languages = ["Python", "Go", "Rust"]
```

<p align="justify">We want to print not only the name, but also its number.</p>

<p align="justify">We could do it like this:</p>

```python
for i in range(len(languages)):
    print(i, languages[i])
```

<p align="justify">It works, but it looks a bit like a workaround. We get the length of the list, build a <em>range()</em>, and then use the index to access the list again.</p>

<p align="justify">Python has <em>enumerate()</em> for this:</p>

```python
for i, language in enumerate(languages):
    print(i, language)
```

<p align="justify">Result:</p>

```text
0 Python
1 Go
2 Rust
```

<p align="justify">Essentially, <em>enumerate()</em> adds a counter to each element as you iterate over it.</p>

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

<p align="justify">And this:</p>

```python
for i, language in enumerate(languages):
```

<p align="justify">simply unpacks these pairs into two variables.</p>

<p align="justify">Often, numbering from zero isn't useful at all. For example, if we're displaying a ranking:</p>

```python
languages = ["Python", "Go", "Rust"]

for position, language in enumerate(languages, start=1):
    print(f"{position}. {language}")
```

<p align="justify">We'll get:</p>

```text
1. Python
2. Go
3. Rust
```

<p align="justify">I think this is one of those cases where the code reads almost like ordinary text.</p>

<p align="justify">By the way, the number produced by <em>enumerate()</em> is more accurately called a counter rather than an index. With a regular <em>enumerate(languages)</em>, it matches the list index, but nothing stops us from writing:</p>

```python
enumerate(languages, start=42)
```

<p align="justify">The list itself, of course, won't suddenly start being indexed from 42.</p>

<p align="justify"><strong>zip()</strong></p>

<p align="justify">Now let's look at another common situation.</p>

<p align="justify">We have some names:</p>

```python
names = ["Alice", "Bob", "Charlie"]
```

<p align="justify">And ages stored separately:</p>

```python
ages = [25, 31, 28]
```

<p align="justify">We need to iterate over them at the same time.</p>

<p align="justify">Again, we could use indices:</p>

```python
for i in range(len(names)):
    print(names[i], ages[i])
```

<p align="justify">But this is simpler:</p>

```python
for name, age in zip(names, ages):
    print(name, age)
```

<p align="justify">We'll get:</p>

```text
Alice 25
Bob 31
Charlie 28
```

<p align="justify">The name <em>zip()</em> is quite fitting here. The function sort of zips two sequences together.</p>

```text
Alice    25
Bob      31
Charlie  28
```

<p align="justify">If we look at the result using <em>list()</em>:</p>

```python
list(zip(names, ages))
```

<p align="justify">we'll get:</p>

```text
[
    ("Alice", 25),
    ("Bob", 31),
    ("Charlie", 28),
]
```

<p align="justify">And there can be any number of sequences:</p>

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 31, 28]
cities = ["London", "Berlin", "Madrid"]

for name, age, city in zip(names, ages, cities):
    print(name, age, city)
```

<p align="justify">There's no need to work with indices here anymore.</p>

<p align="justify"><strong>There's one nuance with zip()</strong></p>

<p align="justify">What happens if the lists have different lengths?</p>

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 31]

for name, age in zip(names, ages):
    print(name, age)
```

<p align="justify">Result:</p>

```text
Alice 25
Bob 31
```

<p align="justify">Charlie simply won't make it into the loop.</p>

<p align="justify"><em>zip()</em> stops when the shortest sequence is exhausted.</p>

<p align="justify">Sometimes that's exactly what you want. And sometimes it's a bug you'd rather notice.</p>

<p align="justify">If the lengths must match, you can write:</p>

```python
for name, age in zip(names, ages, strict=True):
    print(name, age)
```

<p align="justify">Then, if the lengths don't match, we'll get a <em>ValueError</em>.</p>

<p align="justify"><strong>zip() is handy for creating dictionaries</strong></p>

<p align="justify">We have a list of fields:</p>

```python
fields = ["name", "age", "city"]
```

<p align="justify">And a list of values:</p>

```python
values = ["Alice", 25, "London"]
```

<p align="justify">We can combine them:</p>

```python
user = dict(zip(fields, values))
```

<p align="justify">And get:</p>

```python
{
    "name": "Alice",
    "age": 25,
    "city": "London",
}
```

<p align="justify">It's a simple technique, but it comes in handy from time to time.</p>

<p align="justify"><strong>And you can use them together</strong></p>

<p align="justify">Suppose we have participants and their scores:</p>

```python
names = ["Alice", "Bob", "Charlie"]
scores = [95, 87, 91]
```

<p align="justify">We want to print:</p>

```text
1. Alice — 95
2. Bob — 87
3. Charlie — 91
```

<p align="justify">Then we can combine both functions:</p>

```python
for position, (name, score) in enumerate(
    zip(names, scores),
    start=1,
):
    print(f"{position}. {name} — {score}")
```

<p align="justify">At first glance, this construction may look a little strange:</p>

```python
position, (name, score)
```

<p align="justify">But if we look at the data, it becomes clearer.</p>

<p align="justify"><em>zip()</em> gives us:</p>

```text
("Alice", 95)
("Bob", 87)
("Charlie", 91)
```

<p align="justify">And <em>enumerate()</em> adds a number to each such pair:</p>

```text
(1, ("Alice", 95))
(2, ("Bob", 87))
(3, ("Charlie", 91))
```

<p align="justify">That's where this unpacking comes from:</p>

```python
position, (name, score)
```

<p align="justify">The main idea here is the same as with many other Python features: if you find yourself manually managing indices, it's worth first checking whether there's a way to express the task directly.</p>

