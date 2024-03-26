---
title: More even issues 9
keywords: sample
summary: "A traves de estos comandos se observa el interior del modelo"
sidebar: product1_sidebar
permalink: p1_sample9.html
folder: product1
---

## logging 


### Dimensionado de gráficas

```cmd
simscape.logging.
sscexplore
sscprintzcs
simscape.logging.plot({simlog1.TS.x simlog2.TS.x},'names',{'Run1' 'Run2'});
```
### Comandos para lanzar simulaciones

```cmd
set_param(mdl,'SimulationCommand','Start')
set_param(mdl,'SimulationCommand','Stop')
set_param(mdl,'SimulationCommand','Pause')
set_param('vdp','SimulationCommand','continue')
set_param('vdp','SimulationCommand','update')
set_param('my_model','StartFcn','openscopes')
```

 buscar dentro de un bloque 
```cmd
'SaveFinalState'
'SaveOperatingPoint'    
'SaveOutput'         
'SaveState'          
'SaveTime'    
```

```cmd
whos("-file",activeConfigObj)%noOK
```



encontrando los valores de los bloques

```cmd
% Type de block
BlockPaths = find_system(mdl,'Type','Block')


formatSpec = ' Name is %s  & number is %i \n';
% display name of blocks
for idx=1:1:length(BlockPaths)
    fprintf(formatSpec,BlockPaths{idx}, idx)
end
% display values

for idx=1:1:length(BlockPaths)
    fprintf('%s',BlockPaths{idx})
    BlockDialogParameters = get_param(BlockPaths{idx},'DialogParameters')
    BlockTypes = get_param(BlockPaths{idx},'BlockType')
end

%% obtener lista de los parametros -- cuadro de dialogo
BlckDialPars13 =get_param(BlockPaths{13},'DialogParameters');
%BlockDialogParameters = get_param('A0_FuelCell_240109model_FMU/FuelCellStack','DialogParameters')


NamesDialPars13 =fieldnames(BlckDialPars13)

for idx=1:1:length(NamesDialPars13)
    fprintf('%s \t %s \n',NamesDialPars13{idx}, get_param(BlockPaths{13},NamesDialPars13{idx}))
end
```
