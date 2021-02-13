---
title: Uso de la consola
keywords: documentation, python, technical writers, help, authoring tools, replacements
last_updated: December 30th, 2020
tags: [formatting]
summary: Here documentation relative console
sidebar: general_sidebar
permalink: gral_usage_console.html
folder: mydoc
output: web, pdf
---

## Instalacion de git bash 

https://www.stanleyulili.com/git/how-to-install-git-bash-on-windows/


## Pasos para usar la consola


Se recomienda renombrar los archivos lo menos posible

Conocer el estado de los archivos en el repositorio
```cmd
git status
```

La salida puede ser la siguiente

```cmd
$ git status
On branch dev_schematics
Your branch is up to date with 'origin/dev_schematics'.

nothing to commit, working tree clean
```

Cuando se ha agregado un nuevo archivo en local los pasos son los siguientes

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

realice el commit del archivo
```cmd
$ git commit -m "new file test"
```

la salida que obtendra

```cmd
[dev_schematics c07d9cf] new file test
 1 file changed, 174 insertions(+)
 create mode 100644 NewFile.drawio
```

de nuevo revise el estado del repositorio

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

La he liao! Que hago?

Para borrar
```cmd
git rm NewFile.drawio
```

Para mover
```cmd
git mv file_old file_new)
```

Recuerde una vez eliminado el archivo o cambiado de direccion debe realizar el paso de commit y push al repositorio web

More detail in [web Asoc Robotica UC3M](https://asrob-uc3m.gitbooks.io/tutoriales/content/software/version-control/git.html#comprobar-estado-de-repositorio-git-**status**)


En resumen

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


<iframe width="560" height="315" src="https://www.youtube.com/embed/ZxTnevdY9lA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


[git atlassian](https://www.atlassian.com/es/git/tutorials/git-bash)
[git examples](https://dzone.com/articles/top-20-git-commands-with-examples)