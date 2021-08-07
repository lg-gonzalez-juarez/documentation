---
title: sample 1
keywords: sample
summary: "Modify repository - git page"
sidebar: product2_sidebar
permalink: p2_sample1.html
simple_map: true
map_name: usermap
box_number: 1
folder: product2
---

Comandos para generar una git page que usa gem especifica

* generar git-page
* habilitar el link publico dentro de mi usuario
* fork theme git-jenkyll
* modify Gemfile (cuidado con la seccion de cada gitpage)
* una vez que los enlaces son correctos en local y servidor, vienen los siguientes comandos
* `gem install`
* `bundle install`
* `bundle exec jekyll build o serve`

importante si se tienen problemas revisar en los releases, las versiones de gem, jekyll, ruby, etc

## Despues de lanzar al servidor 

Se puede ver el comportamiento de la web en tablet y móvil de la siguiente forma

* boton derecho, inspeccionar
* buscar arriba izquierda botoncito movil-tablet


## Comandos para solucionar el problema de *.JPG al exportar de powepoint

Al exportar las diapositivas de un archivo `*.ppt`, en windows las imagenes se generan con la extensión `.JPG`. Esto algunas veces puede causar problemas con las directivas que usa el servidor y que la web al ser publicada rompa. 

Para ello, cambiamos la extensión `.JPG` pot `.jpg` a mano antes de insertarlos en el directorio local de git, o bien si ya lo hemos agregado en el directorio local resolver el problema con los siguientes comandos 

```dos
git mv DT/DT04.JPG digitaltween/slide04.jpg

git add assets/images/digitaltween/slide04.jpg

git commit -a -m "new slides"

git push
```