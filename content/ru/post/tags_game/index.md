---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Пятнашки"
subtitle: ""
summary: "Задача на программирование пятнашек (Python)."
authors: []
tags: [Python]
categories: []
date: 2022-12-05T13:08:49+03:00
lastmod: 2022-12-05T13:08:49+03:00
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
<li class="nav-item"><a href="#игра_в_15" class="nav-link"><span class="section-num">1</span> Игра в 15</a></li>
<li class="nav-item"><a href="#формулировка_задачи_15" class="nav-link"><span class="section-num">2</span> Математика перестановок</a></li>
<li class="nav-item"><a href="#формулировка_задачи_15" class="nav-link"><span class="section-num">3</span> Формулировка задачи</a></li>
<li class="nav-item"><a href="#решение_задачи_15" class="nav-link"><span class="section-num">4</span> Решение</a></li>
</ul>
</nav>
</details>

<h2 id='игра_в_15'><span class="section-num"><b>1</span>. Игра в 15</b></h2>
<p align="justify">В 1878 году Ноем Чепмэном была придумана игра пятнашки (такен). Головоломка состоит из 15 одинаковых квадратных костяшек, лежащих в квадратной коробке. Каждый такой элемент пронумерован. Коробка же имеет размер 4x4 костяшек (1 квадратик остается пустым). Также могут встречаться и другие вариации этой игры 3x3, 5x5 и другие. Цель игры проста - расположить костяшки по возрастанию номеров, двигая их внутри коробки.</p>
<h2 id='математика_перестановок'><span class="section-num"><b>2</span>. Математика перестановок</b></h2>
<p align="justify">Количество возможных начальных положений пятнашек равно n!</p>

<style>
    .heatMap {
        text-align: center;
    }
    .heatMap th {
        background: grey;
        word-wrap: break-word;
        text-align: center;
    }
    td, th {
    	border: 1px solid black;
    }
    .heatMap td:nth-child(1) { background: #98FB98; }
    .heatMap td:nth-child(2) { background: #B0E0E6; }
</style>

<div class="heatMap" style="text-align: center;">

<center>

| Размер| Число начальных положений | 
|:-----:|:-------------------------:|
| 2x2   | 24                        |
| 2x4   | 40 320                    |
| 3x3   | 362 880                   |

</center>

</div>

<p align="justify">Ровно в половине из всех возможных начальных положений пятнашек невозможно привести к собранному виду. <a href="https://mathworld.wolfram.com/15Puzzle.html" target = "_blank">Подробнее здесь.</a></p>



<h2 id='формулировка_задачи_15'><span class="section-num"><b>3</span>. Формулировка задачи</b></h2>

<p align="justify">Дано 2 матрицы: изначальная и конечная. Реализовать решение задачи (осуществляя <a href="https://en.wikipedia.org/wiki/Depth-first_search" target = "_blank">поиск в глубину</a>), применяя <a href="https://ru.wikipedia.org/wiki/Эвристический_алгоритм" target = "_blank">эвристику</a>.</p>

<h2 id='решение_задачи_15'><span class="section-num"><b>4</span>. Решение</b></h2>
<p align="justify">Для просмотра решения на языке Python вы можете посетить <a href="https://github.com/Jexari/intelligent-systems" target = "_blank">мой репозиторий</a>.</p>
