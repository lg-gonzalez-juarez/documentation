---
title: Usage FEniCS
keywords: documentation, help
last_updated: July 17th, 2021
tags: [formatting]
summary: welcome page
sidebar: general_sidebar
permalink: gral_usage_fecnis.html
folder: gral
output: web, pdf
---

En este apartados se tienen los pasos a seguir para instalar y usar FEniCS en una maquina virtual bajo el sistema operativo Linux y usando como entorno de programación Visual studio code

En este ejemplo el sistema operativo host corresponde a win2 10 y el sistema operativo del guest corresponde a ubuntu 20.4 LTS


# 0. Habilitación de virtualización del equipo



# 1. Instalación máquina virtual

Lo primero que se necesita es descargar la máquina virtual

[oficial site download virtualbox](https://www.virtualbox.org/wiki/Downloads)

- Al instalar, seleccionar el idioma en ingles e instalar ubuntu en el pc

- Seleccionar el idioma de entrada del teclado emplear en español

- durante la instalación habilite la opción de install "third-party software..."
  
 Nota: estos pasos pueden verse en el siguiente video

<iframe width="560" height="315" src="https://www.youtube.com/embed/x5MhydijWmc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# 2 Instalar la guess additions

[download oficial](http://download.virtualbox.org/virtualbox/4.0.0/)

descargar el archivo `VBoxGuestAdditions_4.0.0.iso`


El pack extensión se puede emplear para mejorar la compatibilidad y gestión de interfaces entre el equipo host y el equipo guess. Esto a través de "mount guest extension iso" en el caso de usar la consola de ubuntu. O bien también se puede realizar usando la  pestaña del host. Se lanza ejecutable en guest.



una vez que se ha montado la imagen (archivo extension iso). Ejecutar el siguiente comando


```cmd
sudo apt-get install virtualbox-guest-utils virtualbox-guest-x11 virtualbox-guest-dkms
```

una vez se ha ejecutado el comando reiniciar ubuntu


# 3. Instalación de FEniCS
Instalar fenics por consola

```cmd
sudo apt install fenics
```




Descargar visual studio code *.dev
Instalar
-	Copiar el nombre del folder

```cmd
cd Downloads
sudo apt install ./”namefolder”
```

Pasos para usarlo
Ir a la carpeta que te guste
```cmd
Code .
```
**Notesé saltar espacio entre code y punto**

