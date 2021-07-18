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


## 0. Habilitación de virtualización (VT) del PC

La opción de habilitar la virtualización depende del equipo. En el siguiente link se da una amplia explicación acerca de este punto: [¿puedo habilitar la virtualización de mi equipo?](https://support.bluestacks.com/hc/es/articles/115003910391--C%C3%B3mo-puedo-habilitar-la-virtualizaci%C3%B3n-VT-en-mi-PC-). En el caso de mi PC, se accede a la **PC BIOS** por la tecla fnc+f2, o bien f2. Se adjunta captura de pantalla del objetivo final de este paso.


{% include image.html file="/virtualmachine/VTx_myPC02.png" alt="VTx" caption="This is my enabled VTx" %}



## 1. Instalación máquina virtual

Lo primero que se necesita es descargar la máquina virtual, [oficial site download virtualbox](https://www.virtualbox.org/wiki/Downloads)

- Al instalar, seleccionar el idioma en ingles e instalar ubuntu en el pc

- Seleccionar el idioma de entrada del teclado emplear en español o bien ingles.De forma personal recomiendo en ingles por tema de tutoriales y foros de ayuda en su mayoria domina el ingles.

{% include image.html file="/virtualmachine/screenshot_installubuntu.jpg" url="https://www.virtualbox.org/wiki/Downloads" alt="download virtualbox" caption="Process Instalation" %}


- Durante la instalación habilite la opción de install "third-party software..."

{% include image.html file="/virtualmachine/options_install_ubuntu.png" url="https://www.virtualbox.org/wiki/Downloads" alt="download virtualbox" caption="Options of Process Instalation" %}

{% include image.html file="/virtualmachine/options_install_ubuntu_02.png" url="https://www.virtualbox.org/wiki/Downloads" alt="download virtualbox" caption="Options of Process Instalation" %}


**Los pasos de instalación descritos pueden verse en el siguiente video**

<iframe width="560" height="315" src="https://www.youtube.com/embed/x5MhydijWmc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Notas de esta sección**

- En caso de instalar en teclado en ingles, el cambio a teclado en español se realiza con el siguiente comando
  
```cmd
setxkbmap es,es
```

## 2 Guest Additions & Pack Extensions

Los pack extensions y las guess additions se puede emplear para mejorar la compatibilidad y gestión de interfaces entre el equipo host y el equipo guess. Esto a través de "mount guest extension iso" en el caso de usar la consola de ubuntu. O bien también se puede realizar usando la  pestaña del host. Se lanza ejecutable en guest & host, según las necesidades y caracteristicas del equipo.


### 2.1 Instalar la guess additions

Descargar el archivo `VBoxGuestAdditions_4.0.0.iso` del sitio [download oficial](http://download.virtualbox.org/virtualbox/4.0.0/).


{% include image.html file="/virtualmachine/install_guestAdditions.png" url="http://download.virtualbox.org/virtualbox/4.0.0/" alt="download guest additions" caption="Options of Guest Addition Process Instalation" %}


Para montar la iso de instalación seguir los pasos mostrados en [link proceso instalación Guest Addition win10](https://pureinfotech.com/install-guest-additions-windows-10-virtualbox/).


En caso de obtener algún error.... "if you get an error saying the guest system has no CD-ROM, stop the virtual machine, open the virtual machine settings and from the “Storage” tab, add a new CD-ROM device to the machine by clicking on the plus sign (Adds optical device)"

{% include image.html file="/virtualmachine/correcciónISO_guestAdditions.png" url="http://download.virtualbox.org/virtualbox/4.0.0/" alt="download guest additions" caption="Error Correction of Guest Addition Process Instalation" %}


En caso de obtener de nuevo error se recomienda instalarlo desde la consola nativa por comando de consola.

{% include image.html file="/virtualmachine/error_install_GuestAdditions.png" url="http://download.virtualbox.org/virtualbox/4.0.0/" alt="download guest additions" caption="Options of Guest Addition Process Instalation" %}


Dado que se se ha montado la imagen (archivo extension iso) en el paso anterior solo es necesario ejecutar el siguiente comando

```cmd
sudo apt-get install virtualbox-guest-utils virtualbox-guest-x11 virtualbox-guest-dkms
```

Una vez se ha ejecutado el comando reiniciar Ubuntu. Debería verse algo similar a la siguiente captura de pantalla:

{% include image.html file="/virtualmachine/working_guestAdditions.png" url="http://download.virtualbox.org/virtualbox/4.0.0/" alt="download guest additions" caption="EXIT Guest Addition Process Instalation" %}

Una vez reiniciado el Ubuntu y la máquina virtual, la opción de portapapeles direccionales se habilita en la pestaña de dispositivos. **A disfrutar de Ubuntu virtualizado** 🥁

## 3. Instalación de FEniCS

Se recomienda desde comando nativo de Ubuntu lanzar el siguiente comando:

```cmd
sudo apt install fenics
```

## 4. Instalación de Visual Studio Code

Descargar del sitio web [descarga oficial Visual Studio Code](https://code.visualstudio.com/). Descargar el archivo con extension **.dev**

{% include image.html file="/visualstudiocode/download_dev.png" url="https://code.visualstudio.com/" alt="download Visual Studio Code" caption="Visual Studio Code Process Instalation" %}

-	Copiar el nombre del folder (por ejemplo code_1.58.2-1626302803_amd64.deb)

-	Ejecute los siguientes comandos en consola nativa

```cmd
cd Downloads
sudo apt install ./code_1.58.2-1626302803_amd64.deb
```
Puede suceder que el nombre el sistema operativo lo índice cortado, en el mensaje de error indicará la longitud del truncado (p.ej. quitando el .deb y/o algo más)

- Pasos para usarlo
Ir a la carpeta que te guste, por ejemplo en 

```cmd

cd wk 
```

```cmd
code .
``` 

**Notesé el espacio entre code y punto**, porque funciona mejor pillando carpeta entera (con subcarpetas) y además se integra mejor con git y código.

Si se ejecuta Python desde la consola nativa de ubuntu (consola bash) emplee el comando 

```cmd
Python nombre.py
```

En el caso de programar en consola nativa, recuerde abrir el interprete `ipython`y ejecute copiando+pegando línea a línea el código para ejecutarlo. O bien ejecute a través de las pestañas del propio visual estudio code

## 5. Instalación de Python 3 a través de Visual Studio Code

En la barra izquierda lateral seleccione el cuarto icono y busque de las opciones desplegables `python 3.9.0`. Una vez instalado reinicie Visual Studio Code para actualizar las librerias instaladas y tener una correcta integración en la IDE.

{% include image.html file="/visualstudiocode/install_python3.png" url="https://code.visualstudio.com/" alt="install python 3" caption="Python 3 Code Process Instalation" %}

## 6. Instalación de Git en Ubuntu

- Abrir una terminal y lanzar el siguiente comando

  ```linux
  sudo apt install git
  ```
- Confirmar la instalación de git y revisar la versión instalada

  ```linux
  git --version
  ```
- Definir los parámetros del usuario a nivel global

  ```linux
  git config --global user.name "UserName"
  git config --global user.email "Useremail@UserDomain"
  ```
- Revisar la correcta definición de los ajustes del usuario

```linux
git config --list
```

**NOTA:** El email tiene que ser el mismo que el de la cuenta de GitHub o GitLab según sea la plataforma donde se tiene el repositorio.

{% include image.html file="/visualstudiocode/configuration_git.png" url="https://code.visualstudio.com/" alt="download Visual Studio Code" caption="Visual Studio Code Process Instalation" %}


### 6.1 Clonar la primer rama de un repositorio

- Lanzar el comando de clonado de una rama `git clone -b BranchName  DirectoryRepo`. Por ejemplo para la rama **testing** del repo **Fenics**

```linux
git clone -b testing  https://gitlab.com/capgeminido/fenics
```

{% include image.html file="/visualstudiocode/first_cloneRepoGitLab.png" url="https://code.visualstudio.com/" alt="download Visual Studio Code" caption=" Process Configuration of GitLab" %}

Los pasos de como usar la variedad de comandos disponibles los puede seguir leyendo en la pestaña de esta web [uso de la consola](https://lg-gonzalez-juarez.github.io/Doc/gral_usage_console.html)

