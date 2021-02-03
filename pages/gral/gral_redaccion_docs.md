---
title: Buenas practicas en la redacción de documentos
keywords: documentation, technical writers, 
last_updated: February 2th, 2021
tags: [formatting]
summary: Pautas para una buena redacción
sidebar: general_sidebar
permalink: gral_redaccion_docs.html
folder: gral
output: web, pdf
---

## Herramientas de redacción

Para redactar existe una amplia gama de herramientas entre las que destacan: Microsoft Word, LaTex y Markdown. La selección se deja en función del grado de formalidad del documento y las necesidades/conocimientos del redactor/escritor

- Altran (plantillas documentación)
- UC3M (plantillas docs)
- Circe Templates
- SKD Templates

## Indice del documento

- Una profundidad de índice admisible es hasta 3 subniveles (sección 2.3.4), aunque luego en el documento se desglosen más (sección 2.3.4.c).
- Cantidad de páginas por capítulo compensado (no tiene sentido que un capítulo sea de 80 páginas y otro de 3).
Aquí un ejemplo de índice:
  1. Introducción (con introducción, objetivos, estructura del documento)
  2. Estado del arte A+B+C
  3. Arquitectura global (aquí entra bien un diagrama de flujo general)
  4. Desarrollo A
  5. Desarrollo B
  6. Desarrollo C
  7. Experimentos y resultados
  8. Conclusiones y líneas futuras (con conclusiones y líneas futuras)
- Bibliografía
- Anexos (sí: presupuesto)(posible: partes relevantes de datasheets)(no: códigos fuentes completos, véase sección código fuente).

## Estado del arte

El estado del arte de un documento científico debería consistir en referencias a documentos científicos que componen la Bibliografía, tanto por que sean útiles o porque posteriormente se debata que se hayan superado. También debería servir para explicar alternativas software o hardware, como apoyo para justificar decisiones de diseño que se tomen más adelante en el documento.

## Bibliografía

- Existen muchos gestores de referencias bibliográficas: Mendeley (que dispone de plugins para Microsoft Word y LibreOffice, y puede exportar ficheros .bib para LaTeX), Zotero... En LaTeX se recomienda trabajar con ficheros .bib que genera ficheros .bbl mediante el comando bibtex (frente a la alternativa de directamente manipular los elementos \bibitem del .bbl).
- URLs (blogs, foros, webs...). En principio, tratar de evitar este tipo de referencias bibliográficas. Muchas veces se puede encontrar un documento científico que describe el mismo contenido (p.ej. la wikipedia muchas veces cita artículos científicos como fuente).
- Tratar de utilizar siempre bibliografía científica, que debe componerse principalmente de contenidos de años recientes (aunque puede contener algunas referencias clásicas). En general nuestra proporción será de más proceedings que journals precisamente por la búsqueda de material reciente:
    - Journals: Artículos de revistas científicas. Pasan por procesos de revisión por pares en general largos y con varias iteraciones, por tanto suelen ser largos, descriptivos e informativos. Los journals "top" están indexados en Journal Citation Reports (JCR), donde a su vez cada categoría se desglosa en cuartiles (y el "top" es Q1). En el otro lado del espectro están los journals a evitar, que suelen llamarse Predatory Journals Robótica: IJRR, T-RO...
    - Proceedings de conferencias: Artículos que se presentan en conferencias científicas. En general, con contenido más actual y breve que journals. Los proceedings "top" están indexados en Web of Science (WOS). 
    - Para localizar bibliografía científica, utiliza buscadores como Google Académico o IEEExplore que dispongan de la opción de importar citas a bibtex o semejante.
    - UC3M (acceso a buscadores JCR y WOS): Puedes acceder a los buscadores JCR dentro de Información para investigadores > "ENLACE DE ACCESO DIRECTO A LAS B..." > JCR o WOS
    - UC3M (acceso a buscador de normas UNE): AENORMás UC3M > http://biblioteca3.uc3m.es/RREE/recurso.php?recurso=AENOR
  - UC3M (acceso estos recursos desde fuera de las redes del campus): Las subscripciones de la Biblioteca (p.ej. IEEExplore, JCR y WOS) funcionan de forma automática para dentro de las redes de los campus (cable, WiFi-UC3M, eduroam en campus). Para acceder externamente, puedes utilizar el servicio VPN.
- Véase también la sección de formato de citas bibliográficas.


## Formato (Importante)

- Respecto a títulos de documento/capítulo/secciones: "Esto es un título en español". "This Is A Title In English". Ninguno acaba en punto.
- Como norma general, ceñirse a las plantillas, sin modificar márgenes ni introducir excesivos modificadores de formato. La inclusión de ciertos paquetes de LaTeX también pueden crear conflictos.
- Texto justificado (no alineado a izquierda).
- Evitar faltas de ortografía/gramática.
- Evitar faltas en la puntuación: espacio después de punto, etc. Cuidado en mayúsculas/minúsculas.
- Evitar la reutilización de frases completas de otros documentos (copia+pega). Incluso las licencias más abiertas piden que se cite la fuente original.
- Utilizar frases cortas. Como regla general, se puede pensar "no más de un concepto por frase, tal vez más de una frase para explicar un solo concepto".
- Coherencia interna. Ejemplo 1: MTi debe aparecer siempre como MTi, no MTI a veces. Ejemplo 2: Un algoritmo es siempre un algoritmo, no pasa a ser un método o infraestructura en un mismo documento.
- Evitar extranjerismos sin referenciar (p.e. si el documento está en español, como mínimo poner pie de página ante anglicismos).

## Formato de figuras

- Centradas.
- Sin deformar (conservar proporciones originales).
- Texto explicativo debajo y también centrado.
- Figuras siempre referenciadas. Si es posible, cerca de la propia figura, y antes de aparecer.
Figuras vectoriales. Siempre que se pueda (logotipos, diagramas de flujo, etc) crear y utilizar imágenes de tipo vectorial. Estas imágenes no se pixelan con cambios de zoom. Se recomienda Inkscape como la alternativa libre referencia (existen alternativas propietarias como Adobe Illustrator o Corel). Para generar diagramas, tanto yEd (freeware) como Dia (libre) son buneas opciones (también pensar en https://mermaidjs.github.io/). Powerpoint también puede exportar a formatos vectoriales. LaTeX permite también crear imágenes vectoriales, por ejemplo a través de TikZ. El formato vectorial editable más recomendable es el .svg de Inkscape, o los propios de cada programa. Para incrustar en documentos LaTeX (pdflatex), se recomienda exportar a PDF. Para incrustar en documentos Word, se recomienda exportar a EMF (o WMF si sale mal)(disponible en versión Windows de Inkscape).
- A veces debemos volver a generar las referencias cruzadas para que se actualice el orden.
- Un buscador para imágenes libres: http://search.creativecommons.org/
- UC3M: Aquí un enlace con logos en vectorial: https://github.com/asrob-uc3m/recursos-digitales/tree/master/logos

## Formato de bibliografía

- Es necesario que todos los elementos de la bibliografía estén referenciados.
- La regla general es citar la referencia sólo la primera vez que aparece. Excepciones: no se introduce en el resumen/abstract (sí en la introducción); se puede volver a citar cuando ha pasado un cierto número de páginas (p.ej. capítulos diferentes).
- Se deja un espacio entre la palabra y la referencia, como se hace en esta frase [1]. Es recomendable, además, que esta frase pueda leerse habiendo omitido la referencia (p.antiejemplo: léase [3] y [16]).
- Existen diversos formatos para citar (APA, etc). Para aquellos que son numéricos, el orden de los elementos debe ser el de aparición en el documento (a veces debemos volver a generar las referencias cruzadas para que se actualice)(nota: ciertos autores prefieren orden alfabético).
- URLs: Se comentó en bibliografía que se debe tratar de evitar este tipo de referencias bibliográficas. En caso de ser realmente necesario, es obligatorio poner la fecha de acceso: "(último acceso 22 de febrero de 2011)", y es preferible que sea un pie de página en lugar de un elemento de la bibliografía como tal.

## Formato de ecuaciones

- Referencias entre paréntesis (no corchetes).

## Formato de tablas

- Centradas.
- Texto explicativo normalmente encima y también centrado.

## Código fuente

- Bulto de código fuente: La tendencia es no incluir bultos de código en una memoria, ni siquiera como anexo. Se sube a un lugar y se proporcional la URL.
- Fragmentos de código fuente: Los fragmentos de código fuente en teoría no deberían ir como figuras. Específicamente, en LaTex, se suele utilizar el mecanismo listing. listing tiene muchas opciones, incluida la de poner un marco alrededor y sintaxis (pone colores cual IDE, indicándole si es Python, JSON, etc).
- Recomendación: Incluir diagramas (de flujo, UML, etc), que sí son figuras (y aplican las recomendaciones de la sección figuras). Para trabajos con software en lenguajes de programación orientados a objetos (OOP), los diagramas de clases son casi indispensables.
- También es un plus incluir un enlace a la documentación generada por Doxygen (que además se puede configurar para generar distintos diagramas).


## Úlitmos consejos

- Revisar enlaces rotos y referencias internas rotas (p.ej. buscar por ?? en LaTeX/, buscar error en Microsoft Word)
- Revisar, en todas las páginas generadas por LaTeX/Microsoft, que ninguna palabra se haya salido de márgenes (el hyphen puede hacer que esto ocurra con parabras muy largas)
- Se empezó a realizar un script que revisa textos en inglés aquí ([permalink](https://github.com/jgvictores/snippets/blob/8db93e72b29279ffa959e5b72287ab8e0129fa16/bash/review-tex.sh)).
- ¡Releer el documento entero mínimo una vez!

## Más enlaces de interés

- [Pautas para una buena presentación](http://wiki.asrob.uc3m.es/index.php/Presentar)
- [Uso de Git](https://asrob-uc3m.gitbooks.io/tutoriales/content/software/version-control/git.html)
- [Redaccion en Markdown](https://asrob-uc3m.gitbooks.io/tutoriales/content/writing/markdown.html)
<!--  Extractred from -- >
<!-- https://asrob-uc3m.gitbooks.io/tutoriales/content/writing/redactar.html  -->