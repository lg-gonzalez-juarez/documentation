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

dentro de este archivo se modifica en la cabecera del mismo el campo **permalink:** `Name.html`

El nombre del archivo se debe incluir en el indexado, esto se realiza en la carpeta **_data/sidebars/mydoc_sidebar.yml**

en este archivo se debe actualizar el titulo de la sección y su correspondiente **url**

Por último compruebe que la correspondiente seccion se ha añadido correctamente al navegador lateral

## About Python Pypower

Python is a interpreter

## About usage python pypower

Here describe some example, and

download and unpack the tarball and install:

```python
git clone http://github.com/rwl/PYPOWER.git
python setup.py installl
```

[Doc Api](https://rwl.github.io/PYPOWER/api/) contained main commands of API PyPower

[github-pages PyPower](https://rwl.github.io/PYPOWER/usage.html#application-programming-interface)



{% include links.html %}
