---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Git Basics"
subtitle: ""
summary: "What is Git? Basic commands for version control."
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
<summary class="font-weight-bold">Content</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#about_git" class="nav-link"><span class="section-num">1</span> What is Git and what is it for?</a></li>
<li class="nav-item"><a href="#main_commands" class="nav-link"><span class="section-num">2</span> Basic commands</a></li>
<li class="nav-item"><a href="#dictionary" class="nav-link"><span class="section-num">3</span> Dictionary</a></li>
</ul>
</nav>
</details>

<h2 id='about_git'><span class="section-num"><b>1</span>. What is Git and what is it for?</b></h2>
<p align="justify">What is <a href="https://git-scm.com/" target = "_blank">Git</a> for, and what is a version control system anyway? A version control system is a system that records changes to a file or set of files over time and allows you to revert to a specific version later. Simply put, in case of a file change, the file and the place of the change will be marked, you can also undo the previously entered file changes, see who last changed something and caused the problem and when, and much more. If you break something or lose files, you can easily fix it.</p>
<p align="justify">One such system is Git. At the moment, it is the most common for a number of reasons:</p>
<ul><li>Free and open source</li>
<li>Fast</li>
<li>Simple branching</li>
<li>Backup</li></ul>
<p align="justify">Hostings are provided for git repositories, for example: GitHub, Codebase, Bitbucket, GitLab, etc.</p>

<h2 id='main_commands'><span class="section-num"><b>2</span>. Basic commands:</b></h2>

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

| Command | Command description | 
| -- | -- |
| git init | creating a new repository |
| git status | view status of current files |
| git add | adding changes and new files to the current directory |
| git add file.py | adding file.py |
| git .add | adding all changes |
| git commit | creating a new commit |
| git commit -m 'text' | creating a commit called text |
| git branch | shows a list of all branches |
| git branch -v | shows a list of branches and the latest commit in each |
| git branch name | creates a new branch name |
| git branch -D name | deletes a branch name |
| git checkout | switching between recent commits |
| git checkout file | revert file to last commit state |
| git config | configuration and options git |
| git config --global user.name | shows username |
| git config --global user.name 'New name' | changes username |
| git config --global user.email | shows the user's email |
| git config --global user.email 'name@gmail.com' | changes the user's email |
| git push | uploading local commits to a remote repository |
| git pull | downloads changes from the remote repository to the local one |
| git clone | cloning a project from a remote repository |
</div>



<h2 id='dictionary'><span class="section-num"><b>3</span>. Dictionary</b></h2>
<h4>Branch</h4>
<p align="justify">A branch or copy of the project where you can make any changes, they will not affect the main project.</p>
<h4>Git</h4>
<p align="justify">How files and their versions are stored.</p>
<h4>Cloning</h4>
<p align="justify">Copying a repository to a hard drive.</p>
<h4>Commit</h4>
<p align="justify">Set with changes (changed, new and added files) written to the local repository.</p>
<h4>Push</h4>
<p align="justify">Sending changes to the server.</p>
