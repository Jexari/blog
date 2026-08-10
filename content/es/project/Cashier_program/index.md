---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Programa para el cajero"
summary: "Está diseñado para automatizar los procesos de venta de productos. Reconoce el producto mediante el código de barras, muestra su precio, registra las ventas y mucho más."
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

<a href="https://github.com/Jexari/Program-for-the-cashier">Puede hacer clic aquí para ver el programa.</a>

<p align="justify"> <strong>Programa para el cajero</strong> es una aplicación educativa de caja registradora desarrollada en Python utilizando Tkinter. El proyecto está diseñado para automatizar las principales operaciones de un cajero: apertura y cierre de turnos, búsqueda de productos mediante código de barras, realización de ventas, control del dinero en el cajón de efectivo y almacenamiento del historial de operaciones. </p>

<p align="justify"> La información sobre los productos se almacena en el archivo editable <code>codes.ods</code>. Para cada producto se especifican el código de barras, el nombre y el precio. El cajero puede escanear o introducir un código de barras, tras lo cual el programa encuentra el producto correspondiente y lo añade a la venta actual. </p>

<p align="justify"> La información sobre las ventas completadas y los turnos de caja se almacena en la base de datos <code>orders.db</code>. Cada venta está vinculada al cajero y al turno abierto, mientras que a los pedidos completados se les asignan automáticamente números con el formato <code>ORD-000001</code>. </p>

<h3>Trabajo con los turnos de caja</h3>

<p align="justify"> Antes de comenzar a trabajar, el usuario selecciona un cajero y abre un turno de caja. Al abrir el turno, se especifica el saldo inicial de dinero en el cajón de efectivo. </p>

<p align="justify"> Durante el turno, el programa registra las ventas y permite registrar manualmente ingresos o retiradas de efectivo. Al cerrar la caja, se introduce la cantidad real contada. El programa calcula el saldo esperado y guarda cualquier posible diferencia. </p>

<p align="justify"> Si la aplicación se cerró antes de finalizar el turno, el turno no cerrado se restaura automáticamente la próxima vez que se inicia el programa. </p>

<h3>Almacenamiento y control de datos</h3>

<p align="justify"> Para verificar la integridad de la base de datos financiera se utiliza una suma de comprobación SHA-256. Al iniciar el programa, el contenido de <code>orders.db</code> se compara con la suma de comprobación guardada en <code>orders.db.sha256</code>. Después de una modificación normal de los datos, la suma de comprobación se actualiza automáticamente. </p>

<p align="justify"> Las principales acciones del programa se registran en el archivo <code>cash_register.log</code>: inicio y cierre de la aplicación, apertura y cierre de turnos, escaneo de productos, realización de ventas, ingresos y retiradas de efectivo, comprobación de la integridad de la base de datos y los errores que se produzcan. El registro puede abrirse directamente desde la interfaz del programa en modo de solo lectura. </p>

<h3>Características principales</h3>

<ul> <li>selección del cajero antes de comenzar a trabajar;</li> <li>apertura y cierre del turno de caja;</li> <li>búsqueda de productos mediante código de barras;</li> <li>realización y almacenamiento de ventas;</li> <li>numeración automática de pedidos;</li> <li>control del efectivo en el cajón de caja;</li> <li>ingreso y retirada de dinero;</li> <li>cálculo del saldo esperado y real de la caja;</li> <li>restauración de un turno no cerrado después de reiniciar el programa;</li> <li>mantenimiento de un registro de acciones;</li> <li>comprobación de la integridad de la base de datos mediante SHA-256;</li> <li>creación de una aplicación autónoma para Windows.</li> </ul>

<h3>Tecnologías</h3>

<p align="justify"> El proyecto está escrito en <strong>Python</strong>. La interfaz gráfica de usuario está creada utilizando <strong>Tkinter</strong>. Para almacenar los datos de los productos se utiliza una hoja de cálculo <strong>ODS</strong>, mientras que las operaciones y la información sobre los turnos de caja se almacenan en una base de datos local. </p>

<p align="justify"> Para Windows está prevista la creación del programa como un archivo independiente <code>CashRegister.exe</code> mediante PyInstaller. La aplicación puede iniciarse sin una ventana de consola, mientras que los archivos de trabajo se crean y almacenan junto al archivo ejecutable. </p>

<h3>Objetivo del proyecto</h3>

<p align="justify"> El objetivo principal del proyecto es desarrollar una aplicación de escritorio independiente que simule el funcionamiento de un puesto de trabajo de caja y poner en práctica el trabajo con una interfaz gráfica de usuario, el almacenamiento local de datos, los turnos de caja, el registro de operaciones y el control de la integridad de los datos. </p>
