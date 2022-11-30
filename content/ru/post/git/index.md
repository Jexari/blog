---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Основы работы с Git"
subtitle: ""
summary: "Что такое Git? Основные команды для контроля версий."
authors: []
tags: [Git]
categories: [Git]
date: 2022-05-07T18:44:49+03:00
lastmod: 2022-05-07T18:44:49+03:00
featured: true
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
<li class="nav-item"><a href="#about_git" class="nav-link"><span class="section-num">1</span> Что такое Git и для чего он нужен?</a></li>
<li class="nav-item"><a href="#main_commands" class="nav-link"><span class="section-num">2</span> Основные команды</a></li>
<li class="nav-item"><a href="#dictionary" class="nav-link"><span class="section-num">3</span> Словарь </a></li>
</ul>
</nav>
</details>

<h2 id='about_git'><span class="section-num"><b>1</span>. Что такое Git и для чего он нужен?</b></h2>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Для чего нужен <a href="https://git-scm.com/" target = "_blank">Git</a>, и что вообще такое система контроля версий? Система контроля версий – это система, записывающая изменения в файл или набор файлов в течение времени и позволяющая вернуться позже к определенной версии. Проще говоря, в случае изменения файла будет отмечен файл и место изменения, также можно отменить введенные ранее изменения файла, увидеть, кто последний менял что-то и вызвал проблему и когда, и многое другое. Если вы сломали что-то или потеряли файлы, это спокойно можно исправить.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Одной из таких систем является Git. На данный момент она наиболее распространена по ряду причин:</p>
<ul><li>Бесплатная и с открытым кодом</li>
<li>Быстрая</li>
<li>Простое ветвление</li>
<li>Резервное копирование</li></ul>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Для git-репозиториев предоставляются хостинги, например: GitHub, Codebase, Bitbucket, GitLab и др.</p>

<h2 id='main_commands'><span class="section-num"><b>2</span>. Основные команды:</b></h2>

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
    .heatMap td:nth-child(1) { background: #437DD4; }
    .heatMap td:nth-child(2) { background: #FF4940; }
</style>




<div class="heatMap">

| Команда | Описание команды | 
| -- | -- |
| git init | создание нового репозитория |
| git status | просмотр статуса текущих файлов |
| git add | добавление изменений и новых файлов в текущую директорию |
| git add file.py | добавление файла file.py |
| git .add | добавление всех изменений |
| git commit | создание нового коммита |
| git commit -m 'text' | создание коммита с названием text |
| git branch | показывает список всех веток |
| git branch -v | показает список веток и последний коммит в каждой |
| git branch name | создает новую ветку name |
| git branch -D name | удаляет ветку name |
| git checkout | переключение между последними коммитами |
| git checkout file | вернуть file в состояние последнего коммита |
| git config | конфигурация и параметры git |
| git config --global user.name | показывает имя пользователя |
| git config --global user.name 'New name' | изменяет имя пользователя |
| git config --global user.email | показывает email пользователя |
| git config --global user.email 'name@gmail.com' | изменяет email пользователя |
| git push | загрузка локальных коммитов в удаленный репозиторий |
| git pull | загружает изменения с удаленного репозитория в локальный|
| git clone | клонирование проекта из удаленного репозитория |
</div>



<h2 id='dictionary'><span class="section-num"><b>3</span>. Словарь</b></h2>
<h4>Бранч</h4>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ветка или копия проекта, в которую можно вносить любые изменения, они не повлияют на основной проект.</p>
<h4>Гит</h4>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Способ хранения файлов и их версий.</p>
<h4>Клонирование</h4>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Копирование репозитория на жесткий диск.</p>
<h4>Коммит</h4>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Набор с изменениями (измененными, новыми и добавленными файлами), записанный в локальный репозиторий.</p>
<h4>Пуш</h4>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Отправка изменений на сервер.</p>
