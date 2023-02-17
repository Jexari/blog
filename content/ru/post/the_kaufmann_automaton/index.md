---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "NK-автоматы С. Кауффмана"
subtitle: ""
summary: "Задача на создание автомата С. Кауффмана (Python)."
authors: []
tags: [Python]
categories: []
date: 2022-12-04T23:11:14+03:00
lastmod: 2022-12-04T23:11:14+03:00
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
<li class="nav-item"><a href="#about_the_kaufmann_automaton" class="nav-link"><span class="section-num">1</span> Что такое автомат Кауффмана и как он работает?</a></li>
<li class="nav-item"><a href="#problem" class="nav-link"><span class="section-num">2</span> Формулировка задачи</a></li>
<li class="nav-item"><a href="#solution" class="nav-link"><span class="section-num">3</span> Решение </a></li>
</ul>
</nav>
</details>

<h2 id='about_the_kaufmann_automaton'><span class="section-num"><b>1</span>. Что такое автомат Кауффмана и как он работает?</b></h2>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NK-автомат является сетью из N булевых логических элементов. Каждый логический элемент имеет K входов и один выход. Сигналы на входах и выходах элементов бинарны (принимают значения 0 либо 1). Выходы одних элементов поступают на входы других, эти связи абсолютно случайны, но число входов K каждого элемента статично. Логические же элементы также выбираются случайно.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Автоматы автономны (внешние входы отсутствуют). Число логических элементов, входящих в автомат, предполагается большим, N>1. Автомат функционирует в дискретном времени: t = 1,2,3,… Состояние автомата в каждый момент времени t определяется вектором X(t) – совокупностью выходных сигналов всех логических элементов.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;В процессе функционирования последовательность состояний сходится к аттрактору – предельному циклу. Последовательность состояний X(t) в этом аттракторе может рассматриваться как “программа” функционирования автомата.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Число аттракторов M и типичная длина аттрактора L – важные характеристики NK-автоматов.</p>

<h2 id='problem'><span class="section-num"><b>2</span>. Формулировка задачи</b></h2>
<p>Входные данные:</p>
<ul><li>задать n=4, к=2</li>
<li>задать начальный вектор (напр. int v0[] = {1, 1, 0, 1, 0, 0})
<li>задать матрицу связей, например:

int n[1] = {0, 1, 0, 1, 0, 0}; 

int n[2] = {1, 0, 1, 0, 0, 0}; 

int n[3] = {0, 1, 0, 1, 0, 0}; 

int n[4] = {1, 0, 0, 0, 0, 1}; 

int n[5] = {0, 0, 0, 0, 1, 1}; 

int n[6] = {0, 0, 1, 0, 1, 0}; </li>
<li>Также необходимо описать логические элементы.</li></ul>
<p>Выходные данные:</p>
<ul><li>количество различных аттракторов.</li></ul>

<h2 id='solution'><span class="section-num"><b>3</span>. Решение</b></h2>
<p align="justify">Для просмотра решения на языке Python вы можете посетить <a href="https://github.com/Jexari/intelligent-systems" target = "_blank">мой репозиторий</a>.</p>
