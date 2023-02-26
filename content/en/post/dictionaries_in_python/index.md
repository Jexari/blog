---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Dictionaries in Python"
subtitle: ""
summary: "Everything about dictionaries in Python and nothing more."
authors: []
tags: [Python]
categories: [Python]
date: 2022-12-01T22:21:10+03:00
lastmod: 2022-12-01T22:21:10+03:00
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

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In this entry, we will talk about such a data type as a dictionary. What it is? A dictionary is a data structure in which information is stored in a key-value format. Here I will explain how to access the information stored in a dictionary and how to edit this information, talk about the main methods of dictionaries and how to use them.</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Let's create 2 dictionaries, one stores information about students' grades, the other contains a list of students who eat in the canteen (Fig. 1.1). The dictionary is written in curly brackets. It can either contain initial data (<i>students_marks</i>) or be empty (<i>student_who_eat_in_dining_room</i>).</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As mentioned earlier, all information in dictionaries is stored in the key-value format. If we need to get the value assigned to a particular key, we can do it directly or through the <i>get()</i> method. If the key we entered is missing, then the <i>get()</i> method will return <i>None</i>, but the call without it will give an error. This is important to consider when creating projects where it is not known for sure whether a key with the same name exists in the dictionary.</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We can also add new keys and values, as well as change the values already in the dictionary. All the actions described above and their result can be seen in Fig. 1.1-1.2.</p>

<img align="middle" src="1_1.jpg">
<p align="middle">Figure. 1.1. Program listing 1</p>
<img align="middle" src="1_2.jpg">
<p align="middle">Figure. 1.2. Program output 1</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Consider two other methods, namely <i>keys()</i> and <i>values()</i>. The first returns us all the keys in the dictionary, the second returns all the values, such as <i>dict_keys</i> and <i>dict_values</i> respectively. If we need to remove a pair from a dictionary, we can use <i>del</i> or <i>pop ()</i>. To display all key-value pairs, you need the <i>items()</i> method.</p>

<img align="middle" src="2_1.jpg">
<p align="middle">Figure. 2.1. Program listing 2</p>
<img align="middle" src="2_2.jpg">
<p align="middle">Figure. 2.2. Program output 2</p>

* * *

<p align="justify">To view these and other Python programs, you can visit <a href="https://github.com/Jexari/python_for_site" target = "_blank">my repository</a>.</p>
