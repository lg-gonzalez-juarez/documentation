---
title: Synchronous Machine Simulation
keywords: sample
summary: ""
sidebar: product1_sidebar
permalink: p1_sample3.html
folder: product1
---

## Proceso de Modelado 

En los siguientes directorio se tiene:
- Modelado del motor
- Medidas PQ
- Datos del motor

```matlab
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\MyComputePrg\MtrSincr')
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\MyComputePrg\medidas')
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\DataSheet');dtGenSin31300V_v1
```


### Modelado de las ecuaciones 

Se emplea el modelo de octavo orden

```matlab
% Calculate operating characteristics of synchronous machine
function [sys,x0,str,ts]=SynMachine8th(t,x,u,flag,d,ini)
% State variables       x:      [flux_d flux_fd flux_1d flux_q flux_1q flux_2q inc_wr delta]
% Inputs                u:      [ed efd eq Tm]
% Outputs               y:      [id ifd iq inc_wr delta Te]
% Inicial conditions    ini:    [flux_d flux_fd flux_1d flux_q flux_1q flux_2q inc_wr delta]
switch flag,
    case 0, [sys,x0,str,ts]=mdlInitializeSizes(d,ini);
    case 1, sys=mdlDerivatives(t,x,u,d);
    case 3, sys=mdlOutputs(t,x,u,d);
    case {2,4,9},   sys=[];
    otherwise,   error(['Unhandled flag=',num2str(flag)]);
end

function [sys,x0,str,ts]=mdlInitializeSizes(d,ini)
 global invL 
    sizes = simsizes;     sizes.NumContStates  =8;    sizes.NumDiscStates  =0;
    sizes.NumOutputs     =6;   sizes.NumInputs      =4;    sizes.DirFeedthrough =0;
    sizes.NumSampleTimes =1;    sys = simsizes(sizes);    x0=ini;     str=[];       ts=[0 0]; 
    L_d=[-d.Ld d.Lad d.Lad;-d.Lad d.Lffd d.Lad;-d.Lad d.Lad d.L11d];
    L_q=[-d.Lq d.Laq d.Laq;-d.Laq d.L11q d.Laq;-d.Laq d.Laq d.L22q];
    L=[L_d zeros(3);zeros(3) L_q];
    invL=inv(L);
        
function sys=mdlDerivatives(t,x,u,d)   
 global invL
i_total=invL*x(1:6);
id=i_total(1);ifd=i_total(2);i1d=i_total(3);iq=i_total(4);i1q=i_total(5);i2q=i_total(6);
Te=x(1)*iq-x(4)*id;
wr=1+x(7); %wr=1pu+inc_wr
dflux_d=d.w_base*(u(1)+x(4)*wr+d.Ra*id);
dflux_fd=d.w_base*(u(2)-d.Rfd*ifd);
dflux_1d=d.w_base*(-d.R1d*i1d);
dflux_q=d.w_base*(u(3)-x(1)*wr+d.Ra*iq);
dflux_1q=d.w_base*(-d.R1q*i1q);
dflux_2q=d.w_base*(-d.R2q*i2q);
dinc_wr=(u(4)-Te-d.Kd*x(7))/(2*d.H);
ddelta=x(7)*d.w_base;
sys=[dflux_d;dflux_fd;dflux_1d;dflux_q;dflux_1q;dflux_2q;dinc_wr;ddelta];

function sys=mdlOutputs(t,x,u,d)
global invL 
i_total=invL*x(1:6);
id=i_total(1);ifd=i_total(2);iq=i_total(4);
Te=x(1)*iq-x(4)*id;
wr=1+x(7); %wr=1pu+inc_wr
sys=[id;ifd;iq;x(7);x(8);Te];
```

importante este modelo depende el que se usa


### Inicialización del modelo 

```matlab
%Valores de consigna.
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\MyComputePrg\MtrSincr')
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\MyComputePrg\medidas')
addpath('D:\wk_matlab\uc3m\mt\pc104\Matlab\DataSheet');dtGenSin31300V_v1
%ini=[flux_d0;flux_fd0;flux_1d0;flux_q0;flux_11q0;flux_22q0;inc_wr0;delta0];

ed0=0.5993;  eq0=0.8005;     
P0=1;     Q0=0;   delta0=0;  % valores consigna
efd0=0;   Tm0=0;    % estos valores deben ser cero

disp(sprintf('\t 1).  Operating Point Specifics Define '));
disp(sprintf('\t \t \t-  Stator P0=  %d',P0));
disp(sprintf('\t \t \t-  Stator Q0= %d',Q0));
disp(sprintf('\t \t \t- delta0  = %d ',delta0));
disp(sprintf('\t  Unknown: efd0 Tm0 '));  

NameModel='SymMtrSin8th';
Model_spec = operspec(NameModel) ; % obtiene el punto de operacion

NameBlockOutAdd='SymMtrSin8th/out2';
Model_spec=addoutputspec(Model_spec,NameBlockOutAdd,1);
Model_spec=addoutputspec(Model_spec,NameBlockOutAdd,2);
Model_spec=addoutputspec(Model_spec,NameBlockOutAdd,3);

Model_spec.States(1).Known= [0 0 0 0 0 0 0 1]'; 
Model_spec.States(1).x = [0 0 0 0 0 0 0 delta0]';

Model_spec.Input(1).Known = 1; Model_spec.Input(1).u = 0;
Model_spec.Input(2).Known = 0; Model_spec.Input(2).u = efd0;
Model_spec.Input(3).Known = 1; Model_spec.Input(3).u = 0;
Model_spec.Input(4).Known = 0; Model_spec.Input(4).u = Tm0;
%[P0 Q0 delta0]
Model_spec.Outputs(1).Known=1; Model_spec.Outputs(1).y= P0;
Model_spec.Outputs(2).Known=1; Model_spec.Outputs(2).y= Q0;
Model_spec.Outputs(3).Known=0; Model_spec.Outputs(3).y=delta0;

[Model_op,op_report]=findop(NameModel,Model_spec);
ini=Model_op.States.x; 
efd0= Model_op.Input(2).u
Tm0 = Model_op.Input(4).u
```


En esta parte se tiene la inicialización, con la función `addoutputspec` y se calcula con el comando `findop`.


### Salida de la inicializacion

Al ejecutar este script se tiene como salida lo siguiente:









### Funciones a reutilizar en matlab

 - las condiciones iniciales se tienen en `\pc104\MTLB\bin\MyComputePrg\AsignCondIni`
 - modelado de las ecuaciones iniciales esta en `\pc104\MTLB\bin\MyComputePrg\AsynMach`

### Maquina sincrona
{% raw %}
```html
pc104\MTLB\bin\MyComputePrg\MtrSincr
```
{% endraw %}


### Codigo bueno en ``
{% raw %}
```html
pc104\MTLB\src
```
{% endraw %}

### Last update control
{% raw %}
```html
pc104\MTLB\src\CTR
```
{% endraw %}



## Parámetros de la máquina 

`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\StateStable`


- D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\StateStable_ok2021



### Inicialización de la máquina sincrona


`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\MySyncGnrt\model_ok_Junio2011`

finalmente encontrado y operativo
`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\MySyncGnrt\model_ok_Junio2011_ok2021`


### Diseño del sistema de control

revisar estos archivos
`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\CheeMunOng`


Este es el folder bueno que usamos para los italianos

`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\Kundur `


### Curva de capabilidad

{% raw %}
```html
pc104\MTLB\src\capability
```
{% endraw %}


{% include links.html %}
