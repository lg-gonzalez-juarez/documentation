---
title: Initial concepts
keywords: documentation, python, technical writers, help, authoring tools, replacements
last_updated: December 30th, 2020
tags: [formatting]
summary: Here documentation relative python
sidebar: general_sidebar
permalink: gral_test_lg.html
folder: mydoc
output: web, pdf
---

## About this ...

Esta web tiene el fin de ayudar y ayudarme a tener notitas de todo lo que aprendo en python, si le es útil a alguien mas ya es una ganancia.

<!--
Antes que nada, algunas lineas acerca de mi, soy Lorena Gonzalez-Juarez, soy una terricola con dos hogares, el primero por derecho de nacimiento y el disfrutar de ella mientras se trabaja.
-->

[personal git link](https://github.com/lg-gonzalez-juarez)
 
La siguiente pagina es super útil para documentar [course on API documentation](http://idratherbewriting.com/learnapidoc/).  
 

## How add a new section & page?

El primer paso es generar un archivo "Name.md" en la carpeta `\pages\mydoc`

dentro de este archivo se modifica en la cabecera del mismo el campo **permalink:** `Name.html`

El nombre del archivo se debe incluir en el indexado, esto se realiza en la carpeta **_data/sidebars/mydoc_sidebar.yml**

en este archivo se debe actualizar el titulo de la sección y su correspondiente **url**

Por último compruebe que la correspondiente seccion se ha añadido correctamente al navegador lateral

## Install jekill on windows
If you've never installed or run a jekill site locally on your computer, follow these instructions to install:

*[Install jekill on Windows][mydoc_install_jekyll_on_windows]


### Jekyll help

* [Jekyll Talk](https://talk.jekyllrb.com)

* [Jekyll documentation](http://jekyllrb.com/docs/home/)

* [Jekyll on Stack Overflow](http://stackoverflow.com/questions/tagged/jekyll)

* [Jekyll on my blog](http://idratherbewriting.com/category-jekyll/)

## Formatos para tipos de mensajes

{% include warning.html content="Remember, Python is a interpreter language." %}

{% include note.html content=" 
There a excellent blog on technical writing called <a alt='technical writing blog' href='http://idratherbewriting.com'>I'd Rather Be Writing</a>. If you'd like to stay updated with the latest trends, best practices, and other methods for writing documentation, consider <a href='https://tinyletter.com/tomjoht'>subscribing</a>. I also have a site on <a href='http://idratherbewriting.com/learnapidoc'>writing API documentation</a>." %}

{% include important.html content="Is important keep and record info." %}

{% include callout.html content="This is my **danger** type callout. It has a border on the left whose color you define by passing a type parameter." type="danger" %}

{% include callout.html content="This is my **default** type callout. It has a border on the left whose color you define by passing a type parameter." type="default" %}

{% include callout.html content="This is my **primary** type callout. It has a border on the left whose color you define by passing a type parameter." type="primary" %}

{% include callout.html content="This is my **success** type callout. It has a border on the left whose color you define by passing a type parameter." type="success" %}

{% include callout.html content="This is my **warning** type callout. It has a border on the left whose color you define by passing a type parameter." type="warning" %}

{% include callout.html content="**Important information**: This is my callout. It has a border on the left whose color you define by passing a type parameter. I typically use this style of callout when I have more information that I want to share, often spanning multiple paragraphs. <br/><br/>Here I am starting a new paragraph, because I have lots of information to share. You may wonder why I'm using line breaks instead of paragraph tags. This is because Kramdown processes the Markdown here as a span rather than a div (for whatever reason). Be grateful that you can be using Markdown at all inside of HTML. That's usually not allowed in Markdown syntax, but it's allowed here." type="primary" %}

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i> This is a special tip about some file to download....</div>
