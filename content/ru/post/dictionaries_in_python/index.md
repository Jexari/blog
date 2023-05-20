---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Словари в Python"
subtitle: ""
summary: "Все про словари в языке Python и ничего лишнего."
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

<p align="justify">В этой записи речь пойдет о таком типе данных, как словарь. Что это такое? Словарь - это структура данных, в которой информация храниться в виде «ключ — значение». Здесь я расскажу, как получить доступ к информации, хранящейся в словаре, и как редактировать эту информацию, расскажу об основных методах словарей и как их использовать.</p>

<p align="justify">Создадим 2 словаря, в одном хранится информация об оценках учеников, в другом список учащихся, кто ест в столовой (рис.1.1). Словарь прописывается в фигурных скобках. Он может как содержать изначальные данные (<i>students_marks</i>), так и быть пустым (<i>student_who_eat_in_dining_room</i>).</p>

<p align="justify">Как говорилось ранее, вся информация в словарях хранится в формате «ключ — значение». Если нам необходимо получить значение присвоенное определенному ключу, то мы можем сделать это напрямую или через метод <i>get()</i>. В случае, если ключ введенный нами отсутствует, то метод <i>get()</i> вернет нам <i>None</i>, а вот обращение без него выдаст ошибку. Это важно учитывать при создании проектов, где точно не известно, есть ли ключ с таким именем в словаре.</p>

<p align="justify">Мы также можем добавлять новые ключи и значения, а также изменять значения уже имеющиеся в словаре. Все действия, описанные выше, и их результат можно увидеть на рис. 1.1-1.2. </p>

<img align="middle" src="1_1.jpg">
<p align="middle">Рис. 1.1. Листинг программы 1</p>
<img align="middle" src="1_2.jpg">
<p align="middle">Рис. 1.2. Вывод программы 1</p>

<p align="justify">Рассмотрим два других метода, а именно <i>keys()</i> и <i>values()</i>. Первый возвращает нам все ключи в словаре, второй все значения, типа <i>dict_keys</i> и <i>dict_values</i> соответственно. Если нам необходимо удалить пару из словаря возпользуемся <i>del</i> или <i>pop ()</i>. Для вывода всех пар «ключ — значение» нужен метод <i>items()</i>.</p>

<img align="middle" src="2_1.jpg">
<p align="middle">Рис. 2.1. Листинг программы 2</p>
<img align="middle" src="2_2.jpg">
<p align="middle">Рис. 2.2. Вывод программы 2</p>

* * *

<p align="justify">Для просмотра этих и иных программ на языке Python вы можете посетить <a href="https://github.com/Jexari/python_for_site" target = "_blank">мой репозиторий</a>.</p>
