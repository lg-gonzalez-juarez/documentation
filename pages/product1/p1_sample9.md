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

## Parametros del sim solver de matlab

```cmd
simOut = sim('vdp','SimulationMode','normal',...
            'SaveState','on','StateSaveName','xout',...
            'SaveOutput','on','OutputSaveName','yout',...
            'SaveFormat', 'Dataset');
outputs = simOut.yout
```

## logging

```cmd
simscape.logging.
sscexplore
sscprintzcs
simscape.logging.plot({simlog1.TS.x simlog2.TS.x},'names',{'Run1' 'Run2'});
```


## obtener los datos de un archivo *.mat


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



## comandos para lanzar simulaciones

```cmd
% set_param(mdl,'SimulationCommand','Start')
set_param(mdl,'SimulationCommand','Stop')
set_param(mdl,'SimulationCommand','Pause')
set_param('vdp','SimulationCommand','continue')
set_param('vdp','SimulationCommand','update')
set_param('my_model','StartFcn','openscopes')
```

## apps _> Model Linearizer.

steady state manager

Find the operating point that meets these specifications.

```cmd
op = findop(mdl,opspec);
```
## Open & run simulation commands

load & open Model
```cmd
mdl='B0_ee_fuel_cell_iv_ch';
open_system(strcat(mdl,'.slx'))
load_system(strcat(mdl,'.slx'))
```

## get general parameters of configuration model

```cmd
% Get Root Parameter Names

RootParameterNames = fieldnames(get_param(0,'ObjectParameters'));
%ModelParameterNames = fieldnames(get_param(mdl,'ObjectParameters'));

ModelParameterNames = fieldnames(get_param(mdl,'ObjectParameters'));
GlobalParameterNames = setdiff(RootParameterNames,ModelParameterNames)

% open dialog of configurarion parameters
myConfigObj = getActiveConfigSet(gcs);
%  openDialog(myConfigObj);
activeConfigObj = getActiveConfigSet(mdl);

fieldnames(get_param(activeConfigObj,'ObjectParameters'))

% working OK
get_param(activeConfigObj,'StopTime')
get_param(activeConfigObj,'SolverType')
get_param(activeConfigObj,'SolverName')
get_param(activeConfigObj,'FixedStep')
get_param(activeConfigObj,'LoadInitialState')
get_param(activeConfigObj,'SaveFinalState')

get_param(activeConfigObj,'SignalLoggingName') %logsout_eeFCchars
get_param(activeConfigObj,'AlgebraicLoopMsg')
get_param(activeConfigObj,'MinStepSizeMsg')

get_param(activeConfigObj,'LoggingToFile')
get_param(activeConfigObj,'LoggingFileName')

get_param(activeConfigObj,'LoggingIntervals')
get_param(activeConfigObj,'SignalLogging')

%set_param(mdl,'SignalLogging','on')

%get_param(activeConfigObj,'-full')

% No existen por el momento
%{
get_param(activeConfigObj,'InitFcn')
get_param(activeConfigObj,'SimulationTime')
get_param(activeConfigObj,'InitialState')
%}

% new configuration
%{
newConfigObj = copy(activeConfigObj);
set_param(newConfigObj,'Name','ConfigCopy');
attachConfigSet(model, newConfigObj);
set_param(newConfigObj,'SolverType','Fixed-step');

setActiveConfigSet(model,'ConfigCopy');
activeConfigSet = getActiveConfigSet(model);
get_param(activeConfigSet,'Name')

set_param(referencedConfigObj,'SignalLogging','off');

set_param(referencedConfigObj,'StartTime','10');

%}

```

## ver debajo de la mascara de un bloque en Simulink

```cmd
mdlsignals = find_system(gcs,'FindAll','on','LookUnderMasks','all',...
        'FollowLinks','on','type','line','SegmentType','trunk');
ph = get_param(mdlsignals,'SrcPortHandle')
for i=1: length(ph)
    get_param(ph{i},'datalogging')
end
```

## open "Simulation Data Inspector TOOL"
```cmd
Simulink.sdi.view
```

## modificar el valor de resistor por parametros

simIn = Simulink.SimulationInput(mdl);

```cmd
% update de value automatly
% old value=2.55e5

nameBlckA=strcat(mdl,'/Constant1')

simIn = setBlockParameter(simIn,nameBlckA,...
	"Value","3e5");
```


## modificar el valor de resistor por parametros

```cmd
nameBlckB=strcat(mdl,'/Resistor')
get_param(nameBlckB,'DialogParameters')

SetPointValues = 1:50:100;
spv_length = length(SetPointValues);

for i = spv_length:-1:1
    in(i) = Simulink.SimulationInput(mdl);
    in(i) = in(i).setBlockParameter(nameBlckB,...
        'R',num2str(SetPointValues(i)));
end

%out = parsim(in,'ShowSimulationManager','on','ShowProgress','on')

simOut = parsim(in,'ShowSimulationManager','on','ShowProgress','on')
props = who(simOut)

logsout_A = get(simOut(:,1),'logsout_eeFCchars')
logsout_B = get(simOut(:,2),'logsout_eeFCchars')
logsoutL1 = getElement(logsout_A,'watts')
logsoutL2 = getElement(logsout_B,'watts')

% comparative de ambos
figure

plot(logsoutL2.Values.Time,logsoutL2.Values.Data,...
    logsoutL1.Values.Time,logsoutL1.Values.Data)

legend(num2str(SetPointValues(2)),num2str(SetPointValues(1)))


%{
logsoutL1.Values
yout = find(simOut,"yout")
outputX1 = getElement(yout,'watts')
outputX1.Values.Data
%}

% old manner
%{
simIn = Simulink.SimulationInput(mdl);
simIn = setBlockParameter(simIn,nameBlckB,"R","100");
simOut = sim(simIn);
props = who(simOut)
simMetadata = getSimulationMetadata(simOut)
%}

%% analizando los resultados
%{
% 'logsout_eeFCchars'
logsout = get(simOut,'logsout_eeFCchars')
logsoutL1 = getElement(logsout,'watts')
logsoutL1.Values
yout = find(simOut,"yout")
outputX1 = getElement(yout,'watts')
outputX1.Values.Data
%}
```