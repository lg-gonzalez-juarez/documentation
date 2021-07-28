---
title: Hardware in the loop
keywords: sample
summary: "comandos empleados en la integración de labview, dSPACE, Opal-RT con MatLab"
sidebar: product1_sidebar
permalink: p1_sample4.html
folder: product1
---


## Open Modelica integración con Python


https://askubuntu.com/questions/1248743/installation-of-openmodelica



https://openmodelica.org/doc/OpenModelicaUsersGuide/latest/ompython.html

https://openmodelica.org/download/download-linux

Temas importantes 

- En cuanto a la instalación se tiene el mismo problema que con dockers, conflicto con la instalacion por las APA (install PIP, propias de cada app)

- vinculo de las variables de entornos en win2, mitico problema al no ser administradores
  

Solucion temporal usar la maquina virtual que tengo, probado y de momento bien


### Instalación en ubuntu LTS 2020

```cmd
sudo apt install openmodelica 
```

En mi caso, noto que el pc va corto de espacio, reviso como andamos

```cmd
df -lh
```

revisando que todo bien con openmodelica

```cmd
omc
```

comenzando a trabajar con openModelica

```cmd
OMEdit
```

El paquete para enlazar python con openModelica es OMPython

```cmd
 pip install -U https://github.com/OpenModelica/OMPython/archive/master.zip
```

manos a la obra....

```cmd
ipython3
```


y comienza el testing de comandos de un ejemplo 

```cmd
import OMPython 
from OMPython import OMCSessionZMQ  
omc = OMCSessionZMQ()   
omc.sendExpression("getVersion()")  
omc.sendExpression("cd()")

omc.sendExpression("loadModel(Modelica)")             

omc.sendExpression("loadFile(getInstallationDirectoryPath() + \"/share/doc/omc/testmodels/BouncingBall.mo\")")   

omc.sendExpression("instantiateModel(BouncingBall)")    

from OMPython import ModelicaSystem    

model_path=omc.sendExpression("getInstallationDirectoryPath()") + "/share/doc/omc/testmodels/" 

mod=ModelicaSystem(model_path + "BouncingBall.mo","BouncingBall")  

mod=ModelicaSystem(model_path + "BouncingBall.mo","BouncingBall",["Modelica"]) 


mod=ModelicaSystem(model_path + "BouncingBall.mo","BouncingBall",commandLineOptions="-d=newInst") 
mod.buildModel()       

mod.getQuantities()       
mod.getParameters()
mod.getParameters(["c","radius"]) 
mod.getParameters(["e","radius"])  
mod.getSimulationOptions()
```


## HIL


### Leer archivos o datos desde otro pc
    
     - Entras por escritorio remoto al pc[44] 
     - Los archivos que deseas ejecutar los tienes pc[104] 
     -Abres matlab en pc[44] -Ejecutas el siguiente ejemplo: 
     
```cmd
     dir='\\tsclient\D\MTLB\proc\StateEstimator\amediaslos2primeros';   
     addpath(dir);     
```
     
wls_34nudos
y listo se ejecuta el programa sin tenerlo en tu pc

```cmd     
     addpath(genpath('C:\MATLAB\R2012a\toolbox\matpower4.1'))
```     
     
### to set ubuntu: transforn toeps desde 104 desde otro pc (HIL-LAB)

```cmd  
     [102]D:\lggj\code_dspace\20120222_CtrStatComBalanceado\caract 
     destine='\\tsclient\D\THESIS\CODE\plots_eps2pdf'; 
     copyfile(NameFile,destine) 
```     
     
### LECTURA / ESCRITURA DE ARCHIVO 

```cmd     
     x = 0:.1:1;     
     y = [x; exp(x)]; fid = fopen('exp.m','w');     
     fprintf(fid,'Es letra:'); 
     fprintf(fid,'%6.2f %12.8f\n',y); 
     fclose(fid)
```
    http://arantxa.ii.uam.es/~iama/ficheros.pdf
    


{% include links.html %}
