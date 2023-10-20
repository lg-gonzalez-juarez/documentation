---
title: Matlab Usage
keywords: documentation, matlab, technical writers, help, authoring tools, replacements
last_updated: Oct 20th, 2023
tags: [formatting]
summary: Here documentation relative python
sidebar: general_sidebar
permalink: gral_usage_matlab.html
folder: mydoc
output: web, pdf

---

## What you’ll Do


## links de interes 

- Convert state-space representation to transfer function
https://es.mathworks.com/help/matlab/ref/ss2tf.html


- Compute state-space model of linear electrical circuit
https://es.mathworks.com/help/physmod/sps/powersys/ref/power_statespace.html


- Tuning of a Digital Motion Control System
https://es.mathworks.com/help/control/ug/tuning-of-a-digital-motion-control-system.html


- MIMO Control System
https://es.mathworks.com/help/control/ug/build-a-model-of-a-multi-input-multi-output-mimo-control-system.html

- Pedro Lapique
- Pedro Galindo
- Alex Seic

- motor contraroratorio
- generador contrarotativo
- 20, 50,300 magna
- bos
- bifasico coaxial sin rotor


## commandos 

### Python

### Pypower

### Organize code   
D:\wk_matlab\uc3m\mt\pc104\MTLB\bin\MyComputePrg\iniCond

condiciones iniciales de la maquina
D:\wk_matlab\uc3m\mt\pc104\MTLB\bin\MyComputePrg\iniCond


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




## Segunda parte


{% include callout.html content="startup.m" type="warning" %}

```matlab
addpath('C:\PROGRA~2\GAMESA\OCSTOOL\r2012b')
addpath('C:\PROGRA~2\GAMESA\OCSTOOL\r2012b\src')
addpath('C:\PROGRA~2\GAMESA\OCSTOOL\r2012b\src\Bladed_cosim')
addpath('C:\PROGRA~2\GAMESA\OCSTOOL\common')
addpath('C:\PROGRA~2\GAMESA\OCSTOOL')

addpath(genpath('C:\SVN\PCA\ControllerDLL\trunk'))
cd('C:\SVN\PCA\ControllerDLL\trunk')
disp('-----------------')
{% include links.html %}
```

