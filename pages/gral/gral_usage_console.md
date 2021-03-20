---
title: Uso de la consola
keywords: documentation, technical writers, help, authoring tools, console
last_updated: March 20th, 2021
tags: [console]
summary: Here documentation relative console
sidebar: general_sidebar
permalink: gral_usage_console.html
folder: mydoc
output: web, pdf
---

## Instalación de git-bash 
<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i> Download click here <a alt='git to windows' href='https://gitforwindows.org'>git to windows</a></div>


 - [About installation & Guide Git-bash](https://www.stanleyulili.com/git/how-to-install-git-bash-on-windows/)

## Configuración de git-bash

Seguir las instrucciones indicadas en la documentación oficial de git-lab

- [Comenzar a usar GitLab](https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html)
- [Configure your environment](https://docs.gitlab.com/ee/university/training/topics/env_setup.html)


## Pasos para usar la consola


### Recomendaciones generales en el uso de archivos

#### Renombrar los archivos lo menos posible
#### Conocer el estado de los archivos en el repositorio
  
```cmd
git status
```
La salida generada por el comando anterior puede ser la siguiente

```cmd
$ git status
On branch dev_schematics
Your branch is up to date with 'origin/dev_schematics'.

nothing to commit, working tree clean
```

#### Una vez añadido archivo en local, ...
- Una vez añadido el archivo en la dirección local, los pasos son los siguientes

```cmd
git add NewFile.drawio
```

ver de nuevo el estado del repositorio

```cmd
git status
```

la salida obtenida es la siguiente
```cmd
On branch dev_schematics
Your branch is up to date with 'origin/dev_schematics'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   NewFile.drawio
```

#### Realizar commit del archivo
  
```cmd
$ git commit -m "new file test"
```

la salida que obtendra

```cmd
[dev_schematics c07d9cf] new file test
 1 file changed, 174 insertions(+)
 create mode 100644 NewFile.drawio
```

De nuevo revise el estado del repositorio

```cmd
git status
```

La salida que obtendra
```cmd
On branch dev_schematics
Your branch is ahead of 'origin/dev_schematics' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

#### Agregar archivos en repo-web

  Recuerde estos cambios son el local, el paso final es actualizar en su repositorio web
  
```cmd
git push
```
la salida será 

```cmd
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 245 bytes | 245.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote:
remote: To create a merge request for dev_schematics, visit:
remote:   https://gitlab.com/LorenaGonzalezJ/kiw-e/-/merge_requests/new?merge_re
quest%5Bsource_branch%5D=dev_schematics
remote:
To https://gitlab.com/LorenaGonzalezJ/kiw-e
   6bc3e15..c07d9cf  dev_schematics -> dev_schematics
```

finalmente esta sincronizado con el equipo!!!
```cmd
sudo apt-get party
```

#### *La he liao! ¿Qué hago?*

- Para borrar
  
```cmd
git rm NewFile.drawio
```

- Para mover
  
```cmd
git mv file_old file_new)
```

Recuerde una vez eliminado el archivo o cambiado de direccion debe realizar el paso de commit y push al repositorio web

More detail in [web Asoc Robotica UC3M](https://asrob-uc3m.gitbooks.io/tutoriales/content/software/version-control/git.html#comprobar-estado-de-repositorio-git-**status**)


### En resumen

- use "git add/rm <file>..." to update what will be committed
- use "git restore <file>..." to discard changes in working directory
- screen console 
  
  command:
  ```cmd
  clean
  ```
  the keyboard shortcut `ctrl+l`

Eliminar el historial de Git Bash.

```cmd
history -c
```

```cmd
reset  
```

More links


<iframe width="560" height="315" src="https://www.youtube.com/embed/ZxTnevdY9lA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen> </iframe>


[git atlassian](https://www.atlassian.com/es/git/tutorials/git-bash)
[git examples](https://dzone.com/articles/top-20-git-commands-with-examples)

### Clonar un repo

```cmd
git clone DirRepo
```

### Clonar una rama

```cmd
git clone -b NameBranch DirRepo
```

```cmd
git clone -b ACT1 https://gitlab.com/nido-altran/sion/
```

### Cambiar la direccion de un archivo

```cmd
git mv <old name> <new name>
```

### Proceso de generar un nuevo folder

```cmd
mkdir 60_BAT
```

### Proceso de mover archivos

```cmd
git mv test_battery_valores.xls 60_BAT/test_battery_valores.xls

git commit -a -m "New Files at Folder added"

git push 
```

go gitlab and check is changed

<iframe width="560" height="315" src="https://www.youtube.com/embed/-7TDNonrjwA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Cambiar el nombre de un folder

```cmd
git mv openconcept/ 00_openconcept/
```

### Eliminar una rama

El proceso de eliminado se puede realizar desde la webIDE

para revisar en local, se emplea el siguiente comando

```cmd
git branch -a
```

La salida es similar a esto

```cmd
* ACT1
  remotes/origin/ACT1
  remotes/origin/ACT2
  remotes/origin/ACT3
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/patch-1
  remotes/origin/patch-2
```

Ver el estado de las ramas en local y en el repo

```cmd
git fetch -p
```

La salida puede ser similar a

```cmd
warning: redirecting to https://gitlab.com/nido-altran/sion.git/
From https://gitlab.com/nido-altran/sion
 - [deleted]         (none)     -> origin/patch-1
 - [deleted]         (none)     -> origin/patch-2
```

de nuevo se ve el estado del repo

```cmd
git branch -a
```

La salida puede ser similar a

```cmd
* ACT1
  remotes/origin/ACT1
  remotes/origin/ACT2
  remotes/origin/ACT3
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
```
