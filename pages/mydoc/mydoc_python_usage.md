---
title: Python Usage
keywords: documentation, python, technical writers, help, authoring tools, replacements
last_updated: December 30th, 2020
tags: [formatting]
summary: Here documentation relative python
sidebar: mydoc_sidebar
permalink: mydoc_python_usage.html
folder: mydoc
output: web, pdf

---
## Como añadir una nueva seccion - página?

El primer paso es generar un archivo "Name.md" en la carpeta `\pages\mydoc`

dentro de este archivo se coloca en el campo **permalink:** `Name.html`

El nombre del archivo se debe incluir en el indexado, esto se realiza en la carpeta **_data/sidebars/mydoc_sidebar.yml**

en este archivo se debe actualizar su correspondiente **url**

Por último compruebe que la correspondiente seccion se ha añadido correctamente al navegador lateral

{% include links.html %}
