---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Kaufmann's NK-automaton"
subtitle: ""
summary: "The task of creating the Kaufmann's automaton (Python)."
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
<summary class="font-weight-bold">Content</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#about_the_kaufmann_automaton" class="nav-link"><span class="section-num">1</span> What is a Kaufmann's automaton and how does it work?</a></li>
<li class="nav-item"><a href="#problem" class="nav-link"><span class="section-num">2</span> The task formulation</a></li>
<li class="nav-item"><a href="#solution" class="nav-link"><span class="section-num">3</span> The solution of the problem</a></li>
</ul>
</nav>
</details>

<h2 id='about_the_kaufmann_automaton'><span class="section-num"><b>1</span>. What is a Kaufmann's automaton and how does it work?</b></h2>
<p align="justify">The NK-automaton is a network of N Boolean logical elements. Each logic element has K inputs and one output. The signals at the inputs and outputs of the elements are binary (they take the values 0 or 1). The outputs of some elements go to the inputs of others, these connections are absolutely random, but the number of inputs K of each element is static. The logical elements are also chosen randomly.</p>
<p align="justify">Automaton are autonomous (there are no external inputs). The number of logical elements included in the automaton is assumed to be large, N>1. The automaton functions in discrete time: t = 1,2,3,… The state of the automaton at each moment of time t is determined by the vector X(t) – the totality of the output signals of all logic elements.</p>
<p align="justify">In the process of functioning, the sequence of states converges to an attractor - a limit cycle. The sequence of states X(t) in this attractor can be considered as a “program” for the functioning of the automaton.</p>
<p align="justify">The number of attractors M and the typical attractor length L are important characteristics of NK-automaton.</p>

<h2 id='problem'><span class="section-num"><b>2</span>. The task formulation</b></h2>
<p>Input:</p>
<ul><li>set n=4, к=2</li>
<li>set initial vector (e.g. int v0[] = {1, 1, 0, 1, 0, 0})
<li>set a matrix of connections, for example:

int n[1] = {0, 1, 0, 1, 0, 0}; 

int n[2] = {1, 0, 1, 0, 0, 0}; 

int n[3] = {0, 1, 0, 1, 0, 0}; 

int n[4] = {1, 0, 0, 0, 0, 1}; 

int n[5] = {0, 0, 0, 0, 1, 1}; 

int n[6] = {0, 0, 1, 0, 1, 0}; </li>
<li>It is also necessary to describe the logical elements.</li></ul>
<p>Output:</p>
<ul><li>number of different attractors.</li></ul>

<h2 id='solution'><span class="section-num"><b>3</span>. The solution of the problem</b></h2>
For a Python solution, you can visit <a href="https://github.com/Jexari/intelligent-systems" target = "_blank">my repository</a>. 
