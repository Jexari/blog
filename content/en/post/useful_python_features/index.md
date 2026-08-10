---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Python Features Worth Knowing"
subtitle: ""
summary: "Exploring mutable default arguments, *args, **kwargs, LEGB scopes, lambda functions, and type hints with simple examples."
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
<summary class="font-weight-bold">Table of Contents</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#introduction" class="nav-link"><span class="section-num">1</span> Introduction</a></li>
<li class="nav-item"><a href="#mutable-default-arguments" class="nav-link"><span class="section-num">2</span> Mutable default arguments </a></li>
<li class="nav-item"><a href="#args" class="nav-link"><span class="section-num">3</span> *args </a></li>
<li class="nav-item"><a href="#kwargs" class="nav-link"><span class="section-num">4</span> **kwargs </a></li>
<li class="nav-item"><a href="#legb" class="nav-link"><span class="section-num">5</span> Scope and the LEGB rule </a></li>
<li class="nav-item"><a href="#lambda" class="nav-link"><span class="section-num">6</span> Lambda functions </a></li>
<li class="nav-item"><a href="#type-hints" class="nav-link"><span class="section-num">7</span> Type hints </a></li>
<li class="nav-item"><a href="#conclusion" class="nav-link"><span class="section-num">8</span> Conclusion </a></li>
</ul>
</nav>
</details>

<h2 id="introduction">1. Introduction</h2>

<p align="justify" >When you first start learning Python, functions seem fairly simple: pass a few arguments and get a result. But gradually, default values, arbitrary numbers of parameters, nested functions, and type annotations come into play. At this point, it becomes clear that Python functions involve far more mechanics than it might seem at first glance.</p>

<p align="justify" >Most of the things covered in this article are not rare language tricks. On the contrary, they can be found in almost any sufficiently large Python project. That is why it is useful to understand not only the syntax but also what is happening behind it.</p>

<h2 id="mutable-default-arguments">2. Mutable default arguments</h2>

<p align="justify" >Let's start with one of Python's most well-known features — mutable objects used as default function arguments.</p>

<p align="justify" >Suppose we need a function that adds a given value to a list. At first glance, the following code looks perfectly reasonable:</p>

```python
def add_item(item, items=[]):
    items.append(item)
    return items


print(add_item("Python"))
print(add_item("Java"))
```

<p align="justify" >You might expect the result to look something like this:</p>

```text
['Python']
['Java']
```

<p align="justify" >But in fact, the result will be:</p>

```text
['Python']
['Python', 'Java']
```

<p align="justify" >The reason is that a default argument value is not created every time the function is called. It is created once — when the function itself is defined. After that, subsequent calls continue to work with the same object.</p>

<p align="justify" >A list is <em>mutable</em>, meaning it is an object that can be changed. When we call <em>append()</em>, the existing list is modified, and that change is preserved for the next function call.</p>

<p align="justify" >Usually, it is better to write such a function using <em>None</em>:</p>

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items


print(add_item("Python"))
print(add_item("Java"))
```

<p align="justify" >Now, every time the function is called without the second argument, a new list is created inside the function:</p>

```text
['Python']
['Java']
```

<p align="justify" >The same applies to dictionaries, sets, and other mutable objects. For example, using <em>config={}</em> in function parameters can lead to exactly the same behavior.</p>

<p align="justify" >At the same time, this Python behavior can sometimes be used intentionally. For example, it can be used to preserve some state between function calls. However, such code is usually not the most obvious to someone reading it later, so it is better to use more explicit solutions for storing state.</p>

<h2 id="args">3. *args</h2>

<p align="justify" >Usually, the number of function arguments is known in advance:</p>

```python
def add(a, b):
    return a + b
```

<p align="justify" >But sometimes you do not know beforehand how many values will be passed. Python provides the <em>*args</em> construct for this purpose.</p>

```python
def add(*args):
    print(args)


add(1, 2, 3, 4)
```

<p align="justify" >As a result, we get:</p>

```text
(1, 2, 3, 4)
```

<p align="justify" >Inside the function, <em>args</em> is a regular tuple. Therefore, you can work with it just like with any other <em>tuple</em>.</p>

<p align="justify" >For example, we can write a function that adds any number of values:</p>

```python
def add(*args):
    result = 0

    for number in args:
        result += number

    return result


print(add(1, 2))
print(add(1, 2, 3, 4, 5))
```

<p align="justify" >The name <em>args</em> itself is not a special Python keyword. What matters is the asterisk before the parameter name.</p>

<p align="justify" >Technically, the function could also be written like this:</p>

```python
def add(*numbers):
    return sum(numbers)
```

<p align="justify" >However, <em>*args</em> has become a standard convention and is familiar to most Python developers.</p>

<p align="justify" >The asterisk is not only used when declaring a function. It can also be used to unpack a sequence when calling one.</p>

```python
def print_user(name, age):
    print(name, age)


user = ["Alex", 25]

print_user(*user)
```

<p align="justify" >This call is effectively equivalent to the following:</p>

```python
print_user("Alex", 25)
```

<p align="justify" >This kind of unpacking is convenient when the arguments are already stored inside a list or tuple.</p>

<h2 id="kwargs">4. **kwargs</h2>

<p align="justify" >While <em>*args</em> allows a function to accept an arbitrary number of positional arguments, <em>**kwargs</em> does something similar for keyword arguments.</p>

```python
def show_user(**kwargs):
    print(kwargs)


show_user(name="Alex", age=25, city="Madrid")
```

<p align="justify" >Inside the function, we get a regular dictionary:</p>

```text
{'name': 'Alex', 'age': 25, 'city': 'Madrid'}
```

<p align="justify" >Therefore, values can be accessed in the usual way:</p>

```python
def show_user(**kwargs):
    print(kwargs.get("name"))
    print(kwargs.get("age"))


show_user(name="Alex", age=25)
```

<p align="justify" >As with <em>args</em>, the name <em>kwargs</em> is a convention rather than a required part of the syntax. What matters are the two asterisks.</p>

<p align="justify" ><em>*args</em> and <em>**kwargs</em> are often used together:</p>

```python
def example(*args, **kwargs):
    print("args:", args)
    print("kwargs:", kwargs)


example(1, 2, 3, language="Python", version=3)
```

<p align="justify" >We get:</p>

```text
args: (1, 2, 3)
kwargs: {'language': 'Python', 'version': 3}
```

<p align="justify" >Two asterisks can also be used to unpack dictionaries when calling a function.</p>

```python
def create_user(name, age):
    print(f"{name}: {age}")


user = {
    "name": "Alex",
    "age": 25
}

create_user(**user)
```

<p align="justify" >Python will use the dictionary keys as argument names and the corresponding values as the values of those arguments.</p>

<p align="justify" >This feature is especially useful when working with configurations, decorators, libraries, and wrapper functions, where it may not be known in advance exactly which parameters will need to be passed along.</p>

<h2 id="legb">5. Scope and the LEGB rule</h2>

<p align="justify" >Another important topic in Python is variable scope. If several variables with the same name exist in a program, the interpreter needs to determine which one to use.</p>

<p align="justify" >For this, the <em>LEGB</em> rule is commonly used:</p>

<ul>
<li><em>L — Local</em></li>
<li><em>E — Enclosing</em></li>
<li><em>G — Global</em></li>
<li><em>B — Built-in</em></li>
</ul>

<p align="justify" >Python searches for a name in exactly this order.</p>

<h3>Local</h3>

<p align="justify" ><em>Local</em> is the local scope of the current function.</p>

```python
def example():
    language = "Python"
    print(language)


example()
```

<p align="justify" >The <em>language</em> variable exists inside the function. If you try to access it from outside, Python will not find it.</p>

<h3>Enclosing</h3>

<p align="justify" ><em>Enclosing</em> comes into play when one function is defined inside another.</p>

```python
def outer():
    language = "Python"

    def inner():
        print(language)

    inner()


outer()
```

<p align="justify" >There is no <em>language</em> variable inside the <em>inner()</em> function. Therefore, Python moves to the next level and looks for it in the scope of the <em>outer()</em> function.</p>

<p align="justify" >If we need not only to read such a variable but also to modify it, the <em>nonlocal</em> keyword is used.</p>

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

<p align="justify" >Here, <em>nonlocal</em> tells Python to use the variable from the enclosing function rather than creating a new local one.</p>

<h3>Global</h3>

<p align="justify" ><em>Global</em> is the scope of the current module.</p>

```python
language = "Python"


def show_language():
    print(language)


show_language()
```

<p align="justify" >The function does not find <em>language</em> locally or in an enclosing function, so it reaches the global scope.</p>

<p align="justify" >To modify a global variable inside a function, Python provides the <em>global</em> keyword:</p>

```python
counter = 0


def increment():
    global counter
    counter += 1


increment()
print(counter)
```

<p align="justify" >After the call, the value of <em>counter</em> will be <em>1</em>.</p>

<p align="justify" >At the same time, global variables generally should not be overused. When different functions directly modify shared global state, it becomes more difficult to understand where the current value came from.</p>

<h3>Built-in</h3>

<p align="justify" >The final level is <em>Built-in</em>. This is where Python's built-in names are located, such as <em>print</em>, <em>len</em>, <em>sum</em>, <em>str</em>, and many others.</p>

```python
numbers = [1, 2, 3]

print(len(numbers))
```

<p align="justify" >If you create your own variable with the same name, you can accidentally shadow the built-in function:</p>

```python
len = 10

numbers = [1, 2, 3]

print(len(numbers))
```

<p align="justify" >Now <em>len</em> contains a number rather than the built-in function, so attempting to call it will result in an error.</p>

<p align="justify" >In the end, the rule is quite easy to remember: <em>Local → Enclosing → Global → Built-in</em>. Python moves from the nearest scope to the most general one and stops as soon as it finds the required name.</p>

<h2 id="lambda">6. Lambda functions</h2>

<p align="justify" ><em>Lambda</em> allows you to create small functions without the usual declaration using <em>def</em>.</p>

<p align="justify" >For example, a regular function:</p>

```python
def square(number):
    return number ** 2
```

<p align="justify" >Using <em>lambda</em>, it can be written like this:</p>

```python
square = lambda number: number ** 2

print(square(5))
```

<p align="justify" >The result will be the same in both cases:</p>

```text
25
```

<p align="justify" >The general syntax looks like this:</p>

```python
lambda arguments: expression
```

<p align="justify" >The main limitation is that only one expression can appear after the colon. Therefore, <em>lambda</em> is suitable for small operations rather than a full ten-line function.</p>

<p align="justify" >It is especially convenient when a function is needed only once. For example, when sorting:</p>

```python
users = [
    {"name": "Alex", "age": 27},
    {"name": "Max", "age": 21},
    {"name": "Kate", "age": 24},
]

users.sort(key=lambda user: user["age"])

print(users)
```

<p align="justify" >Here, the function is needed only to tell the <em>sort()</em> method which value should be used to sort the elements.</p>

<p align="justify" >Another common example is using it together with <em>map()</em> or <em>filter()</em>:</p>

```python
numbers = [1, 2, 3, 4, 5]

squares = list(map(lambda number: number ** 2, numbers))

print(squares)
```

<p align="justify" >Result:</p>

```text
[1, 4, 9, 16, 25]
```

<p align="justify" >However, there is no need to shorten code at any cost. If a <em>lambda</em> becomes too long or starts to contain complex logic, a regular function defined with <em>def</em> will almost always be easier to read.</p>

<h2 id="type-hints">7. Type hints</h2>

<p align="justify" >Python is a dynamically typed language. We do not need to declare the type of every variable in advance, and the same variable can refer to objects of different types at different times.</p>

```python
value = 10
value = "Python"
```

<p align="justify" >This is convenient, but in large projects it can sometimes become difficult to understand what data a function expects to receive and what it is supposed to return. This is where <em>type hints</em> — type annotations — are used.</p>

<p align="justify" >For example, a regular function might look like this:</p>

```python
def greet(name):
    return f"Hello, {name}"
```

<p align="justify" >Let's add type information:</p>

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

<p align="justify" >Now the function declaration immediately makes it clear that the <em>name</em> argument is expected to be a string and that the function should return a string.</p>

<p align="justify" >At the same time, Python itself generally does not prevent you from passing a value of another type just because of the annotation.</p>

```python
def greet(name: str) -> str:
    return f"Hello, {name}"


print(greet(123))
```

<p align="justify" >Annotations primarily provide additional information to developers and code analysis tools. IDEs and static analyzers can detect type mismatches before the program is even run.</p>

<p align="justify" >Collections can also be annotated:</p>

```python
def get_names(users: list[str]) -> list[str]:
    return [user.upper() for user in users]
```

<p align="justify" >If a value can have multiple types, modern versions of Python allow you to use the <em>|</em> operator:</p>

```python
def find_user(user_id: int) -> str | None:
    if user_id == 1:
        return "Alex"

    return None
```

<p align="justify" >The <em>str | None</em> notation indicates that the function can return either a string or <em>None</em>.</p>

<p align="justify" >For more complex cases, Python provides the <em>typing</em> module. For example, <em>Callable</em> can be used to describe functions passed as arguments.</p>

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

<p align="justify" >Type hints are especially useful not because they make Python similar to statically typed languages, but because they act as a form of documentation directly inside the code. When a function has five arguments and returns a complex structure, annotations make it significantly easier to read.</p>

<h2 id="conclusion">8. Conclusion</h2>

<p align="justify" >At first glance, the features discussed above may seem almost unrelated. <em>*args</em> and <em>**kwargs</em> deal with passing arguments, <em>LEGB</em> deals with name lookup, <em>lambda</em> is used to create small functions, and <em>type hints</em> help describe expected data types.</p>

<p align="justify" >But all of these mechanisms have one thing in common: they appear constantly in everyday Python code. Without understanding <em>mutable default arguments</em>, it is easy to end up with unexpected state between function calls. Without <em>*args</em> and <em>**kwargs</em>, it is harder to write flexible functions and wrappers. And understanding scopes helps explain where Python gets a variable's value from in the first place.</p>

<p align="justify" ><em>Lambda</em> and <em>type hints</em> are more about making programs easier to write and read. The former provides a compact way to describe small operations, while the latter makes function interfaces significantly clearer.</p>

<p align="justify" >These are far from the only Python features worth knowing. The language also has decorators, generators, context managers, comprehensions, unpacking, <em>property</em>, <em>dataclasses</em>, and many other interesting mechanisms. But those are topics for a separate follow-up.</p>

