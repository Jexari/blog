---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Cashier's work program"
summary: "Designed to automate the processes of selling goods. It recognizes products by barcode, displays their price, records sales, and much more."
authors: [admin]
tags: [Python]
categories: [Python]
date: 2026-06-01T16:48:16+03:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
<a href="https://github.com/Jexari/Program-for-the-cashier">You can click here to view the program.</a>

<p align="justify"> <strong>Program for the Cashier</strong> is an educational cash register application developed in Python using Tkinter. The project is designed to automate the main operations of a cashier: opening and closing shifts, searching for products by barcode, processing sales, accounting for money in the cash drawer, and saving the history of operations. </p>

<p align="justify"> Product information is stored in the editable <code>codes.ods</code> file. A barcode, name, and price are specified for each product. The cashier can scan or enter a barcode, after which the program finds the corresponding product and adds it to the current sale. </p>

<p align="justify"> Information about completed sales and cash register shifts is stored in the <code>orders.db</code> database. Each sale is linked to the cashier and the open shift, while completed orders are automatically assigned numbers in the <code>ORD-000001</code> format. </p>

<h3>Working with Cash Register Shifts</h3>

<p align="justify"> Before starting work, the user selects a cashier and opens a cash register shift. When opening the shift, the initial amount of money in the cash drawer is specified. </p>

<p align="justify"> During the shift, the program records sales and allows manual cash deposits or withdrawals to be registered. When closing the cash register, the actual counted amount is entered. The program calculates the expected balance and saves any possible discrepancy. </p>

<p align="justify"> If the application was closed before the shift was completed, the unclosed shift is automatically restored the next time the program is launched. </p>

<h3>Data Storage and Control</h3>

<p align="justify"> An SHA-256 checksum is used to verify the integrity of the financial database. When the program starts, the contents of <code>orders.db</code> are compared with the saved checksum from <code>orders.db.sha256</code>. After a normal data modification, the checksum is updated automatically. </p>

<p align="justify"> The main actions of the program are recorded in the <code>cash_register.log</code> file: application startup and shutdown, opening and closing shifts, scanning products, processing sales, depositing and withdrawing cash, checking database integrity, and any errors that occur. The log can be opened directly from the program interface in read-only mode. </p>

<h3>Main Features</h3>

<ul> <li>selecting a cashier before starting work;</li> <li>opening and closing a cash register shift;</li> <li>searching for products by barcode;</li> <li>processing and saving sales;</li> <li>automatic order numbering;</li> <li>accounting for cash in the cash drawer;</li> <li>depositing and withdrawing money;</li> <li>calculating the expected and actual cash balance;</li> <li>restoring an unclosed shift after restarting the program;</li> <li>maintaining an activity log;</li> <li>checking database integrity using SHA-256;</li> <li>building a standalone Windows application.</li> </ul>

<h3>Technologies</h3>

<p align="justify"> The project is written in <strong>Python</strong>. The graphical user interface is created using <strong>Tkinter</strong>. An <strong>ODS</strong> spreadsheet is used to store product data, while operations and information about cash register shifts are stored in a local database. </p>

<p align="justify"> For Windows, the program can be built as a separate <code>CashRegister.exe</code> using PyInstaller. The application can be launched without a console window, while working files are created and stored next to the executable file. </p>

<h3>Project Goal</h3>

<p align="justify"> The main goal of the project is to develop a standalone desktop application that simulates the operation of a cashier workstation and to implement, in practice, working with a graphical user interface, local data storage, cash register shifts, operation logging, and data integrity control. </p>
