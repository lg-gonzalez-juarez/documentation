---
title: Initial concepts
keywords: documentation, python, technical writers, help, authoring tools, replacements
last_updated: December 30th, 2020
tags: [formatting]
summary: Here documentation relative python
sidebar: mydoc_sidebar
permalink: mydoc_test_lg.html
folder: mydoc
output: web, pdf
---

Este es mi pinino como documentalista de software (cierta ironia), enfatizo esto tiene el fin de ayudar y ayudarme a tener notitas de todo lo que aprendo en python, si le es útil a alguien mas ya es una ganancia.

Antes que nada, algunas lineas acerca de mi, soy Lorena Gonzalez-Juarez, soy una terricola con dos hogares, el primero por derecho de nacimiento y el disfrutar de ella mientras se trabaja.

[personal git link](https://github.com/lg-gonzalez-juarez)
 
La siguiente pagina es super útil para documentar [course on API documentation](http://idratherbewriting.com/learnapidoc/).  
 
See [my blog's about page](http://idratherbewriting.com/aboutme/) for more details about me.

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

{% include links.html %}
