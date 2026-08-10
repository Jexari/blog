---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "is and == in Python: What's the Difference?"
subtitle: ""
summary: "Understanding the difference between the is and == operators in Python, why they can return different results, and when to use each of them."
authors: [admin]
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
# Associate this post with one or more of your projects.
# Simply enter your project's folder or file name without extension.
# E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
# Otherwise, set `projects = []`.
projects: []

---
<p align="justify">In Python, you can encounter both the <em>==</em> operator and <em>is</em> when comparing values.</p>

<p align="justify">Consider a simple example:</p>

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

<p align="justify">Result:</p>

```text
True
False
```

<p align="justify">The lists <em>a</em> and <em>b</em> contain the same values, so the expression <em>a == b</em> returns <em>True</em>. At the same time, the lists themselves were created separately. They are two different objects, so <em>a is b</em> returns <em>False</em>.</p>

<p align="justify">If we modify the example as follows:</p>

```python
a = [1, 2, 3]
b = a

print(a == b)
print(a is b)
```

<p align="justify">then the result will be different:</p>

```text
True
True
```

<p align="justify">In this case, no new list was created for <em>b</em>. The variable <em>b</em> was assigned a reference to the same object that <em>a</em> already refers to.</p>

<p align="justify">You can also check this using the <em>id()</em> function:</p>

```python
a = [1, 2, 3]
b = a

print(id(a))
print(id(b))
```

<p align="justify">The <em>id</em> values will be the same.</p>

<blockquote>
<p><code>==</code> answers the question: “Do the objects have the same values?”</p>
<p><code>is</code> answers the question: “Is this the same object?”</p>
</blockquote>

## When to Use `==`

<p align="justify">In most ordinary comparisons, the <em>==</em> operator is the one you need.</p>

<p align="justify">For example:</p>

```python
age = 25

if age == 25:
    print("Age matches")
```

<p align="justify">The same applies to strings:</p>

```python
name = "Ian"

if name == "Ian":
    print("Name matches")
```

<p align="justify">And to collections:</p>

```python
a = [1, 2, 3]
b = [1, 2, 3]

if a == b:
    print("Lists are equal")
```

<p align="justify">Here, we are interested in the contents of the objects, not where exactly they are located in memory.</p>

## When to Use `is`

<p align="justify"><em>is</em> makes sense in cases where you need to check object identity.</p>

<p align="justify">The most common example is <em>None</em>:</p>

```python
result = None

if result is None:
    print("No result")
```

<p align="justify">For the opposite check, <em>is not</em> is used:</p>

```python
if result is not None:
    print(result)
```

<p align="justify">This is the form that is usually used in Python code instead of:</p>

```python
if result == None:
    ...
```

## Why `is` Sometimes Works with Numbers and Strings

<p align="justify">Sometimes you may encounter code like this:</p>

```python
a = 10
b = 10

print(a is b)
```

<p align="justify">And get:</p>

```text
True
```

<p align="justify">After this, it may seem that <em>is</em> is perfectly suitable for comparing numbers.</p>

<p align="justify">However, you should not rely on this behavior. Python may reuse some objects that have already been created. This applies, for example, to some integers and strings.</p>

<p align="justify">Therefore, writing:</p>

```python
if number is 10:
    ...
```

<p align="justify">is incorrect.</p>

<p align="justify">You should use:</p>

```python
if number == 10:
    ...
```

<p align="justify">The same applies to strings:</p>

```python
if status == "active":
    ...
```

<p align="justify">and not:</p>

```python
if status is "active":
    ...
```

<p align="justify">The behavior of a program should not depend on whether Python reused an existing object or created a new one.</p>

