---

# Documentation: https://wowchemy.com/docs/managing-content/

title: "Mutable, immutable, and what does hashable have to do with it?"
subtitle: ""
summary: "Understanding the difference between mutable and immutable objects, what hashable means in Python, why a list cannot be used as a dictionary key, and why immutable does not always mean hashable."
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

# Associate this post with one or more of your projects.

# Simply enter your project's folder or file name without extension.

# E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.

# Otherwise, set `projects = []`.

## projects: []
---
<p align="justify">In Python, the concepts of mutable, immutable, hashable, and unhashable often come up together. Especially when talking about lists, tuples, dictionaries, and sets. At first, it's easy to draw a rather simple connection between them: mutable objects cannot be hashed, while immutable ones can.</p>

<p align="justify">In most everyday examples, this does seem to be true. A list is mutable and unhashable, while a string is immutable and hashable. But if we dig a little deeper, it turns out that these are actually different properties of an object.</p>

<p align="justify">Let's start with mutable and immutable.</p>

<p align="justify">Mutable means an object can be changed after it has been created. The most obvious example is a regular list:</p>

```python id="0bjfh6"
numbers = [1, 2, 3]
numbers.append(4)

print(numbers)
# [1, 2, 3, 4]
```

<p align="justify">Here, the list that originally contained three elements now contains four. And importantly, it is still the very same object.</p>

<p align="justify">We can even look at its <em>id</em>:</p>

```python id="ttrm6v"
numbers = [1, 2, 3]

print(id(numbers))

numbers.append(4)

print(id(numbers))
```

<p align="justify">In both cases, the <em>id</em> will be the same. We took an existing object and changed it.</p>

<p align="justify">Strings work differently. Strings in Python are immutable, which means that once they have been created, the object itself cannot be changed.</p>

<p align="justify">For example, this will not work:</p>

```python id="f6lvd5"
name = "cat"
name[0] = "b"
```

<p align="justify">Python will raise a <em>TypeError</em>.</p>

<p align="justify">At the same time, nothing prevents us from writing:</p>

```python id="imfsr1"
name = "cat"
name = "bat"
```

<p align="justify">At first glance, it might seem that we changed the string after all. But we didn't. The variable `name` used to refer to the string <em>"cat"</em>, and after the second assignment it refers to another object — the string <em>"bat"</em>.</p>

<p align="justify">This is an important distinction. Immutable does not mean that a variable cannot be changed. A variable is not the object itself in the first place. Roughly speaking, it is a name that refers to an object. You can change what the name refers to, but you cannot change the immutable object itself.</p>

<p align="justify">The same thing happens with numbers:</p>

```python id="j5n8t8"
x = 10
x += 1
```

<p align="justify">The number <em>10</em> did not turn into <em>11</em>. As a result of the operation, `x` simply started referring to a different value.</p>

<p align="justify">Common mutable built-in types include <em>list</em>, <em>dict</em>, and <em>set</em>. Immutable ones include <em>int</em>, <em>float</em>, <em>bool</em>, <em>str</em>, <em>bytes</em>, <em>tuple</em>, and <em>frozenset</em>.</p>

<p align="justify">And somewhere around this point, another question usually comes up: why can't a list be used as a dictionary key, while a tuple can?</p>

```python id="e1zq46"
data = {
    (10, 20): "point"
}
```

<p align="justify">This is a perfectly valid dictionary.</p>

<p align="justify">But this one:</p>

```python id="x6m04w"
data = {
    [10, 20]: "point"
}
```

<p align="justify">will not even be created:</p>

```text id="i1h71n"
TypeError: unhashable type: 'list'
```

<p align="justify">To understand why, we need to look at what hashable means.</p>

<p align="justify">Python has a built-in function called <em>hash()</em>:</p>

```python id="pdeftw"
hash(42)
hash("hello")
hash((1, 2, 3))
```

<p align="justify">All of these calls work and return some integer. The actual number usually does not matter to us. What matters is that Python can obtain a hash for an object and use it in hash tables, which are used internally by dictionaries and sets, among other things.</p>

<p align="justify">For example, when we write:</p>

```python id="1nm6v1"
users = {
    "alice": 25,
    "bob": 31,
}
```

<p align="justify">Python does not go through every dictionary key from beginning to end each time we access <em>users["alice"]</em>. The key's hash helps Python quickly determine where to look for the corresponding entry.</p>

<p align="justify">This leads to an important requirement: an object's hash must remain stable while the object is being used in this way.</p>

<p align="justify">And this is where it becomes clear why a list would cause problems.</p>

<p align="justify">Let's imagine for a moment that Python allowed us to do this:</p>

```python id="4fnf9e"
key = [1, 2]

data = {
    key: "hello"
}
```

<p align="justify">Python would calculate the hash of <em>[1, 2]</em> and use it to place the entry in a particular location inside the dictionary.</p>

<p align="justify">And then we could do this:</p>

```python id="4a70y6"
key.append(3)
```

<p align="justify">Now our key is <em>[1, 2, 3]</em>.</p>

<p align="justify">If the hash depends on the contents of the list, it would have to change as well. This creates a strange situation: the entry was placed in the dictionary using one hash, but now we would have to look for it using another.</p>

<p align="justify">That is why a regular <em>list</em> simply cannot be hashed:</p>

```python id="8fhf4d"
hash([1, 2, 3])
```

<p align="justify">will result in an error:</p>

```text id="hqm6bj"
TypeError: unhashable type: 'list'
```

<p align="justify">The same applies to <em>dict</em> and <em>set</em>. They are all mutable and therefore are not suitable for regular content-based hashing.</p>

<p align="justify">This is where the useful association comes from:</p>

```text id="n2fnlw"
list  → mutable   → unhashable
dict  → mutable   → unhashable
set   → mutable   → unhashable

str   → immutable → hashable
int   → immutable → hashable
bytes → immutable → hashable
```

<p align="justify">But it is still better not to treat this as a strict rule.</p>

<p align="justify">A good example is <em>tuple</em>.</p>

<p align="justify">A tuple cannot be changed:</p>

```python id="z0a5fx"
point = (10, 20)
point[0] = 100
```

<p align="justify">This will raise an error. So it seems reasonable to expect that a tuple can be hashed:</p>

```python id="57vexd"
point = (10, 20)

print(hash(point))
```

<p align="justify">And indeed, it can.</p>

<p align="justify">Because of this, tuples are convenient to use as dictionary keys. Coordinates are a good example:</p>

```python id="8bc4gk"
places = {
    (40.7128, -74.0060): "New York",
    (51.5074, -0.1278): "London",
}
```

<p align="justify">But now let's put a list inside a tuple:</p>

```python id="eek3if"
value = (1, 2, [3, 4])
```

<p align="justify">The tuple itself is still immutable. We cannot write:</p>

```python id="mvkd87"
value[0] = 100
```

<p align="justify">But nothing prevents us from changing the list inside it:</p>

```python id="k8rgl7"
value[2].append(5)

print(value)
# (1, 2, [3, 4, 5])
```

<p align="justify">Now let's try:</p>

```python id="71ayfn"
hash(value)
```

<p align="justify">and we get a <em>TypeError</em>.</p>

<p align="justify">So a <em>tuple</em> itself is immutable, but that does not guarantee that a particular tuple is hashable. Its elements must also be hashable.</p>

<p align="justify">There is an interesting detail here: the phrase "a tuple cannot be changed" is sometimes taken too literally. You cannot change which objects the tuple's positions refer to. But if a tuple contains a mutable object, such as a list, that object itself can still be changed.</p>

<p align="justify">There is a similar story with sets. A regular <em>set</em> can be changed:</p>

```python id="pdk8j5"
numbers = {1, 2, 3}
numbers.add(4)
```

<p align="justify">Therefore, a <em>set</em> itself is unhashable and cannot be an element of another set.</p>

<p align="justify">But Python also has <em>frozenset</em>:</p>

```python id="th8j9z"
numbers = frozenset({1, 2, 3})

print(hash(numbers))
```

<p align="justify">This is an immutable set, and it can be hashed. Therefore, unlike a regular <em>set</em>, a <em>frozenset</em> can be used as a dictionary key or as an element of another set.</p>

<p align="justify">There is one more rule that helps explain the idea of hashability. If two hashable objects are equal:</p>

```python id="8f6klx"
a == b
```

<p align="justify">then their hashes must also be equal:</p>

```python id="kvrtll"
hash(a) == hash(b)
```

<p align="justify">In other words, if <em>a == b</em>, their hashes must be equal as well.</p>

<p align="justify">The reverse is not true. Two different objects can theoretically have the same hash. This is called a hash collision, and Python knows how to handle such situations.</p>

<p align="justify">In practice, all of this becomes much easier to understand if we don't try to treat mutable and hashable as the same concept.</p>

<p align="justify">Mutable and immutable describe whether an object's state can be changed after the object has been created.</p>

<p align="justify">Hashable and unhashable describe whether an object is suitable for use in Python's hash-based data structures. In practice, this primarily means whether it can be used as a <em>dict</em> key or as an element of a <em>set</em>.</p>

<p align="justify">For standard types, this gives us a fairly familiar picture. Strings, numbers, and suitable tuples can be used as dictionary keys. Lists, dictionaries, and sets cannot.</p>

```python id="4th8u2"
data = {
    "name": "Alice",       # str — allowed
    42: "answer",          # int — allowed
    (10, 20): "point",     # tuple — allowed
}
```

<p align="justify">But this:</p>

```python id="ppzfcq"
data = {
    [10, 20]: "point"
}
```

<p align="justify">will not work.</p>

<p align="justify">And this is probably one of those cases where understanding the reason is more useful than memorizing a table of types. If you remember why a dictionary needs a hash in the first place and why that hash has to remain stable, the behavior of <em>list</em>, <em>tuple</em>, <em>set</em>, and <em>frozenset</em> stops looking like a collection of arbitrary rules.</p>

