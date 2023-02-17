---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "15 Puzzle"
subtitle: ""
summary: "Programming task (Python)."
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
<summary class="font-weight-bold">Content</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#игра_в_15" class="nav-link"><span class="section-num">1</span> 15 puzzle</a></li>
<li class="nav-item"><a href="#формулировка_задачи_15" class="nav-link"><span class="section-num">2</span> The mathematics of permutations</a></li>
<li class="nav-item"><a href="#формулировка_задачи_15" class="nav-link"><span class="section-num">3</span> Task Formulation</a></li>
<li class="nav-item"><a href="#решение_задачи_15" class="nav-link"><span class="section-num">4</span> The solution of the problem</a></li>
</ul>
</nav>
</details>

<h2 id='игра_в_15'><span class="section-num"><b>1</span>. 15 puzzle</b></h2>
<p align="justify">In 1878, Noah Chapman invented the game of 15 puzzle. The puzzle consists of 15 identical square tiles in a square box. Each such element is numbered. The box has a size of 4x4 tiles (1 square remains empty). There may also be other variations of this game 3x3, 5x5 and others. The goal of the game is simple - arrange the tiles in ascending order by moving them inside the box.</p>
<h2 id='математика_перестановок'><span class="section-num"><b>2</span>. The mathematics of permutations</b></h2>
<p align="justify">The number of possible initial positions of the game is n!</p>

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

| Size  | The number of initial positions | 
|:-----:|:-------------------------:|
| 2x2   | 24                        |
| 2x4   | 40 320                    |
| 3x3   | 362 880                   |

</center>

</div>

<p align="justify">In exactly half of all possible initial positions of the 15 puzzle, it is impossible to bring them to an assembled form. <a href="https://mathworld.wolfram.com/15Puzzle.html" target = "_blank">Read more here.</a></p>



<h2 id='формулировка_задачи_15'><span class="section-num"><b>3</span>. Task Formulation</b></h2>

<p>Given 2 matrices: initial and final. Implement a solution to the problem (performing <a href="https://en.wikipedia.org/wiki/Depth-first_search" target = "_blank">a depth-first search</a>), applying <a href="https://ru.wikipedia.org/wiki/Эвристический_алгоритм" target = "_blank">heuristic</a>.</p>

<h2 id='решение_задачи_15'><span class="section-num"><b>4</span>. The solution of the problem</b></h2>
For a Python solution, you can visit <a href="https://github.com/Jexari/intelligent-systems" target = "_blank">my repository</a>. 
