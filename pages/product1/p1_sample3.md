---
title: Synchronous Machine Simulation
keywords: sample
summary: ""
sidebar: product1_sidebar
permalink: p1_sample3.html
folder: product1
---

## Notas acerca del estado del arte de la maquina sincrona

### Lista de libros y modelos



- Fraile Mora
  - resumen de la pagina 416 y 417 reaccion de polos salientes

- Krause control, [Krause,Wasynczuk,Sudhoff]analyisOfElectricalMachineryandDriveSystems
  -  pag 36, circuito de la maquina de polos salientes, 
  -  pag 193 ecuaciones dinamica
  -  linealizacion 316
- - maquina reducida de orden 342,357 

- Chapma, circuito equivalente

- Dynamic Simulation of Electric Machine using Matlab, cheen
      - pag 309, modelo con kd
      - permanent magnets pag 311
      - tres fases, pag 323
      - seis fases,  pag 340-350
      - 

### Modelado mátemático según Krause

De acuerdo a la documentación de matlab, el modelo proporcionado por la toolbox se basa en el libro de krause (Analysis of Electric Machine, página 122, máquina de tres fases, dos polos, de imanes permanentes). Las ecuaciones son las siguientes

$$
\begin{align*}
&\bf{v}_{abc,s}=\bf{r}_s \bf{i}_{abc,s} + p \bf{\lambda}_{abc,s}\\
\bf{\lambda}_{abc,s}&=\bf{L}_s \bf{i}_{abc,s} + \bf{\lambda}^{'}_m\\
T_e&=J\left( \frac{2}{p}p \omega_r \right) + B_m\left( \frac{2}{p}\omega_r \right) + T_L
\end{align*}
$$

**Recuerde p, es el operador derivada**

**NOTE** REVISAR SECCION-> VOLTAGE AND TORQUE EQUATIONS IN ROTOR
REFERENCE-FRAME VARIABLES --> pag 126


Las ecuaciones a implementar son: 4.3-10 hasta 4.3.12


## Modelo basado en kundur
REVISAR ESTO CON ALBERTO EN MODELICA
`D:\wk_matlab\uc3m\mt\pc104\Matlab\Motors\SYNgnrt\Kundur\mdl\aux2`
inicializacion, ok 2021


## Proceso de Modelado 

En este apartado se explica el proceso de inicialización de la máquina. En la figura se presenta la captura de pantalla del modelo realizado en simulink

{% include image.html file="/matlab/mdl_maqsynch_8th.PNG" alt="matlab sim" caption="Simulation machine syncrhonous" %}


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

### Datos del motor

```matlab
% loading machine parameters for synchronous machine
clear all; close all; clc
%...Description Parameters                     
%   Snom => rated power      [VA]        p =>   pair of poles      
%   f    => rated frequency  [Hz]        nr =>  nominal speed  [rpm]
%   Vll  => peak value of rated phase voltage [V]  rms
% MAIN
f_red=50; Sn = 31.3e3 ; Vrms = 400 ; f_base = f_red ; pp=2;
% MACHINE PU
d.Ra=0.04186 ; d.Ll=0.063 ; 
d.Lad=1.497 ; d.Laq=0.717;
d.Rfd=0.02306; d.Lffd=0.1381+d.Lad;
d.R1d=0.1118 ; d.L11d=0.1858+d.Lad;
d.R1q=0.09745 ; d.L11q=0.1258+d.Laq;
d.R2q=0; d.L22q=0.0;
d.H=0.08671; d.Ld=d.Lad+d.Ll; d.Lq=d.Laq+d.Ll;
d.Kd=0;
Ra=d.Ra ; Lad=d.Lad ; Laq=d.Laq;
Ll=d.Ll ; H=d.H; Ld=d.Ld ; Lq=d.Lq;
Rfd=d.Rfd ; Lffd=d.Lffd;
R1d=d.R1d ; L11d=d.L11d;
R1q=d.R1q ; L11q=d.L11q;
R2q=d.R2q ; L22q=d.L22q;
% BASE VALUES
S_base=Sn ; es_base=Vrms*sqrt(2/3);
is_base=2/3*S_base/es_base;
w_base=2*pi*f_base; d.w_base=w_base; %adding w_base to 'd' structure
wm_base=w_base/pp;
Zs_base=es_base/is_base;
Ls_base=Zs_base/w_base;
fluxs_base=Ls_base*is_base;
T_base=S_base/wm_base;
t_base=1/w_base;
%INIT VALUES************************************
%TERMINAL VALUES (per unit)
Pt= 31.3e3/S_base ; Qt=0/S_base;
Ut=1;
It=sqrt(Pt^2+Qt^2)/Ut;
fdp=Pt/Ut/It;
fi=acos(fdp);
%LOAD ANGLE;
delta_i=atan( (Lq*It*cos(fi)-Ra*It*sin(fi) ) / (Ut+Ra*It*cos(fi)+Lq*It*sin(fi)) );
%dq VOLTAGE & CURRENT
Ud_init=Ut*sin(delta_i);       Uq_init=Ut*cos(delta_i);
Id_init=It*sin(delta_i+fi);    Iq_init=It*cos(delta_i+fi);
% field and amortisseur circuits VOLTAGE & CURRENT
Ifd_init=(Uq_init+Ra*Iq_init+Ld*Id_init)/Lad;
Ufd_init=Rfd*Ifd_init;
I1d_init=0 ; I1q_init=0; I2q_init=0;
%MECH
w_init=1 ;
theta_init=-pi/2+delta_i;
Tm_init=Pt+Ra*It^2;

flux_d0=0.698536725;flux_fd0=1.047739435;flux_1d0=0.834806149;
flux_q0=-0.715574206;flux_11q0=-0.66190614;flux_22q0=-0.66190614;
inc_wr0=0;delta0=0.6426;
ini=[flux_d0;flux_fd0;flux_1d0;flux_q0;flux_11q0;flux_22q0;inc_wr0;delta0];
```




### Salida de la inicializacion

Al ejecutar este script se tiene como salida lo siguiente:


```matlab
1).  Operating Point Specifics Define 
	 	 	-  Stator P0=  1
	 	 	-  Stator Q0= 0
	 	 	- delta0  = 0 
	  Unknown: efd0 Tm0 

 Operating Point Search Report:
---------------------------------

 Operating Report for the Model SymMtrSin8th.
 (Time-Varying Components Evaluated at time t=0)

Operating point specifications were successfully met.
States: 
----------
(1.) SymMtrSin8th/Planta
      x:         0.834      dx:      8.72e-15 (0)
      x:          1.03      dx:     -5.45e-15 (0)
      x:         0.872      dx:     -1.56e-14 (0)
      x:        -0.624      dx:      2.18e-15 (0)
      x:        -0.574      dx:      1.53e-14 (0)
      x:        -0.574      dx:            -0 (0)
      x:      1.89e-17      dx:      8.67e-09 (0)
      x:             0      dx:      5.94e-15 (0)

Inputs: 
----------
(1.) SymMtrSin8th/ed
      u:             0
(2.) SymMtrSin8th/efd
      u:        0.0272    [-Inf Inf]
(3.) SymMtrSin8th/eq
      u:             0
(4.) SymMtrSin8th/Tm
      u:          1.04    [-Inf Inf]

Outputs: 
----------
(1.) SymMtrSin8th/out2
      y:             1    (1)
(2.) SymMtrSin8th/out2
      y:      1.67e-15    (0)
(3.) SymMtrSin8th/out2
      y:             0    [-Inf Inf]
```


**NOTA** El código de este apartado se encuentra en `D:\wk_matlab\uc3m\mt\pc104\MTLB\src\Motors\SYNgnrt\MySyncGnrt\model_ok_Junio2011_ok2021`





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


```matlab
%% chech:OK:2015APRIL07
%CHECK:OK:18MAY2013
clear all; close all; clc

%%Edicion to LateX
%{
% Configuracion para los graficos con formato en latex
esq_bajo_izq=0; bajo_dib=0; ancho=16; altura=10; 
Mposition=[esq_bajo_izq bajo_dib ancho altura]; 
%}
iLocLeg='EastOutside';
ColorLine=[0 0 0];
StyleLine='.-|--|-.|:';

set(gcf,'DefaultLineLineWidth',1.5,....
        'DefaultAxesColorOrder',ColorLine,...
      'DefaultAxesLineStyleOrder',StyleLine)

iFontSize=11; iLineWidth=2; jFontSize=9;
%strFontName='Times';
%strFontName='Courier';
%strFontName='ArialBlack';
%strFontName='ModernNo.20';
strFontName='Arial';

set(gcf,'Defaultaxesfontsize',jFontSize,...
    'DefaultAxesFontName','strFontName',...
'DefaultAxesFontUnits','centimeters');
%'DefaultFontWeight','demi'

%--- colocar nombre en los ejes
OBJ01='xlabel(strXlabel);ylabel(strYlabel)'; 
... tamaño y tipo de letra en latex
prop01='FontSize'; prop02='Interpreter'; INprop02='latex';
propA='XLabel'; propB='YLabel';
OBJ02='set(get(gca,propA),prop01,iFontSize,prop02,INprop02)';
OBJ03='set(get(gca,propB),prop01,iFontSize,prop02,INprop02)';
% ---</>

%---- colocar legendas en graficas
OBJ05='legend(strLegend)'; propE='type';  propF='text';
OBJ06='set(findobj(lgOBJ,propE,propF),prop01,jFontSize,prop02,INprop02)';
... color y localizacion de las etiquetas
propG='boxoff'; propH='Location'; propI='edgecolor'; propJ='none';
OBJ07='legend(propG,propH,iLocLeg,propI,propJ)'; 

%ConfigurationPlots
bckGRIS=[.95 .95 .95]; co=[.5 .4 .3]; co01=[.5 .5 .5]; co02=[.7 .7 .7];
posFIG=[509,1071,791,697];
stfC='linewidth';stfA='color';
%% ConvensionGenerador
%% src:stevenson PAGE:98

%---axesTitles
strXlabel='\bf{Potencia Activa P[p.u.]}';
strYlabel='\bf{(fp. en adelanto)|Potencia Reactiva Q[p.u.]|(fp en atraso)}';
strLgnd0={'Límite Estabilidad','Límite de Armadura','Límite de Campo'};
%ylabel(strXlabel,'color','k','fontweight','b') 
%xlabel(strYlabel,'color','k','fontweight','b');
%lead-adelanto  lag-delay

%---DefinitionFUNCTIONS
ShwVls=@(str,in1,in2)eval('disp(sprintf(str,in1,in2))');
LgndVls=@(str,vl)eval('sprintf(str,vl)');%ValueLegendPlot
strAlrm01=['abs(pf) this mus be <= UNO'];
%ShwAlarm=@()eval('warndlg(strAlrm01,'error');')
ShwRing=@()eval('Fs=4096;w=1500;t=0:1/Fs:.15;y=sin(w*t);sound(y,Fs)');
%...
S_pk=@(Va_pk,Ia_pk)(Va_pk*Ia_pk);
angPF=@(pf)(acos(abs(pf)));%angleFactorPower
toDGR=@(ang)(ang*180/pi);
P_pk=@(S_pk,angPF)(S_pk*cos(angPF));
Q_pk=@(S_pk,angPF)(S_pk*sin(angPF));
P_fragm=@(Va,Uexc,Xs)(Va*Uexc/Xs);%PwithoutANGDLTec:3.38
Uexc=@(P,Xs,Va,angDLT)(P*Xs/(Va*sin(angDLT)));%fromEC:3.39
cmplQ=@(Va,Xs)(Va^2/Xs);%termComplementaryEC:3.39CENTRORADIO
angDLT=@(P,Q,cmplQ)(atan(P/(Q+cmplQ)));%fromEC:3.38

%% inputDATA
%[Va,pf,Ia,Xs]=deal(1,0.9,1,2.1);
[Va,pf,Ia,Xs]=deal(1,0.9,1,0.7);
%[Va,pf,Ia,Xs]=deal(1,0.99,1,1.05);%%%%%%%%OK

if abs(pf)>1,warndlg('abs(pf)MUSTbe<=UNO','error');ShwRing,break,end;

A=S_pk(Va,Ia); phio=angPF(pf); pntB=cmplQ(Va,Xs);%pointB-ejeY 

if pf<0, s=-1; else s=1; end

[Po1,Qo1]=deal(P_pk(A,phio),Q_pk(A,phio));
str='%s:%5.3f'; ShwVls(str,'Po1',Po1); ShwVls(str,'Qo1',Qo1);
deltao=angDLT(Po1,Qo1,pntB); 
del1=toDGR(deltao); 
gamo=asin(pntB/A);
phio01=s*toDGR(phio); 
Ef1=Uexc(Po1,Xs,Va,deltao); 

rCC=P_fragm(Va,Ef1,Xs);%radioCurveCap 
bCC=-pntB;%centroCurveCapability
pntR=rCC+bCC;%longitud del arco R

pnt.O.x=0; pnt.O.y=0;%pointOrigen
pnt.Q.x=0; pnt.Q.y=Po1;%pointQ
pnt.P.x=0; pnt.P.y=Qo1;%pointP
pnt.N.x=0; pnt.N.y=bCC;%pointP
pnt.R_b.x=pntR; pnt.R_b.y=bCC;%crucePointM

if del1<0, warndlg('unstableConditions','error');ShwRing,break, end; 

tm=1; 
figure(1);set(gcf,'Position',posFIG);

%PlotPoints
plot(pnt.O.x,pnt.O.y,':k');hold on; 
plot(pnt.O.x,pnt.O.y,'-','color',co01);
plot(pnt.O.x,pnt.O.y,'--','color',co02);

legend(strLgnd0,3);idx=1; %ttlIDX=eval(ttl_idx); %eval(ttlOBJ);
eval(OBJ01); eval(OBJ02); eval(OBJ03);

  disp 'STEP 02: areaCapability'; pause(tm) 

plot([0 A*cos(gamo)],[bCC bCC],':k',stfC,3);%LineStability
%(*1)
phi=-gamo:0.01:s*phio;      x1=A*cos(phi);     x2=A*sin(phi);%Armature 
delta=pi/2-deltao:.01:pi/2; y1=rCC*cos(delta); y2=rCC*sin(delta)+bCC;%Field
 plot(x1,x2,'-',stfA,co01,stfC,3);%Armature(S_pk & phi) 
 pause(2)
 plot(y1,y2,'--',stfA,co02,stfC,3);%field(P_fragm & delta &cmplQ)
 pause(2)
%--AreaSombreada 
a1=[0 A*cos(gamo) x1 y1 pnt.O.x pnt.O.y];%x1-x2:vectores
b1=[bCC+.01 bCC+.01 x2 y2 pnt.R_b.x pnt.R_b.y]; fill(a1,b1,bckGRIS);
%-----------------
disp 'STEP 03: middle & horizontal';pause(tm);
plot([pnt.O.x pnt.O.y],[pnt.R_b.x pnt.R_b.y],'-.k',stfC,2); 
plot([0 1.2*A],[pnt.O.x pnt.O.y],'-.k',stfC,2);%(S_pk)

disp 'STEP 04: lines limit and text'; pause(tm);
plot([pnt.Q.x pnt.Q.y],[bCC Qo1],'color',bckGRIS);
plot([pnt.Q.x pnt.Q.y],[pnt.P.x pnt.P.y],'w');%(S_pk)%PConstant
plot([0 A*cos(gamo)],[pnt.N.x,pnt.N.y],'color',bckGRIS);%(S_pk & cmplQ,fragmP)
%
%-LegendPlots
Qo=LgndVls('%5.3f',Qo1);        Po=LgndVls('%5.3f',Po1)
phio0=LgndVls('%5.2f',phio01);  del=LgndVls('%5.2f',del1);
Ef=LgndVls('%5.3f',Ef1);
%....
text(Po1+.1,Qo1+.1,['Po=',Po,' |\delta_o=',del],'color',co,'fontsize',12)
text(Po1+.1,Qo1,['Qo=',Qo,' |\phi_o=',phio0],'color',co,'fontsize',12)
text(Po1+.2,Qo1-.1,['Ef_o=',Ef],'color',co,'fontsize',12);

disp 'STEP 06: MARK'; pause(tm);

plot(Po1,Qo1,'or','markersize',8,'markerfacecolor','r');%(IaVd)
plot(0,0,'*r','markersize',9); 
plot(0,bCC,'*b','markersize',9);%rCC

disp 'STEP 07: vector'; pause(tm);
vecarrow([0 bCC],[rCC*cos(pi/2-deltao) bCC+rCC*sin(pi/2-deltao)],'k');%Armature
ksttng=0.95;
vecarrow([0 0],[ksttng*A*cos(phio) ksttng*A*sin(s*phio)],'k');%angle 

disp 'STEP 08: text';pause(tm);
text(1.05*A*cos(phio),1.05*A*sin(-phio),'V_aI_a','color',co01);
text(1.05*rCC*cos(1.2),bCC+1.03*rCC*sin(1.2),'V_aE_f/X_s','color',co02);
text(0.04,bCC+.06,'-V_a^2/X_s','color','k'); 
text(.08,bCC+.4,'\delta_o','color','k','fontsize',12); 
text(.15,.04,'\phi_o','color','k','fontsize',12),grid;

axis equal; hold off   %pause(5); close all

%Se genera el vector de puntos a partir del angulo 

%{
set(gcf, 'PaperPositionMode', 'manual');
set(gcf, 'PaperUnits', 'inches');%'centimeters'
set(gcf, 'PaperPosition', [2 1 4 2]);
set(gcf, 'PaperType', 'A4');
%B5-25*18cm
%A5-20.9*14.8
%B3-51*36
%A3
%'arch-A'-OKI
%set(gcf,'PaperOrientation','landscape');%{portrait} 
%set(gcf, 'PaperType', );%OKI
set(gcf, 'PaperPositionMode', 'auto');'manual'   

figure(1); plot(tout,Iabcn_rtr(:,1)/13,'k-',tout,Iabcn_rtr(:,2)/13,'k:',tout,Iabcn_rtr(:,3)/13,'k--','LineWidth',2); %axis([t_ini t_fin -40 40]); 
xlabel('Time [s]','FontSize',20);
ylabel('I_R current [pu]','FontSize',20);  
legend('I_{Ra}','I_{Rb}','I_{Rc}');
set(gca,'FontSize',16,'XTick',[1:0.5:3.5]);
grid; axis([1 3.5 -7 7]); 
print -dpdf 'test01.pdf'; pause(2);% clf; close;
winopen('test01.pdf')
%}

%% Tamaño de la figura y posicion en el monitor
%---- function anonymous para el tamaño del modelo
%{
LBWH=@(LBobj,WHobj) [LBobj(1),LBobj(2),...
    WHobj(1)+LBobj(1),WHobj(2)+LBobj(2)];  
...[left bottom width height]    
%}

%% CONF. texto LATEX
%CnfigDfltPLOTS--archivo con lo anterior
%newDIR='D:\THESIS\CODE\plots_eps2pdf\';%forPRINT
%xo_lim=0; xe_lim=1.1;


%---
%{
nmFIG01='test01'; set(gcf,'name',nmFIG01)
set(0,'Units','centimeters')
monitor_pos=deal(get(0,'MonitorPosition'))
...[left bottom width height] %get(gcf,'Position');   
WHobj=[672,504];  % tamaño figura deseado
LBobj=[-999,520];% donde empieza el bloque
pos_Mdl=LBWH(WHobj,LBobj)
posIN=[-999 680 672 504];%[left bottom width height]
set(gcf,'Position',posIN)
%}

%--- Etiquetas para c/u de las legendas
%{
NameTag='\bf{fp=}';  UnitTag='';
obj_01='legend(strcat(NameTag,num2str(fp(1)),UnitTag),';
obj_02='strcat(NameTag,num2str(fp(2)),UnitTag),';
obj_03='strcat(NameTag,num2str(fp(3)),UnitTag),';
obj_04='strcat(NameTag,num2str(fp(4)),UnitTag))';
obj_=strcat(obj_01,obj_02,obj_03,obj_04);
%--- Titulo para cada subfigura 
ttl_01='\alpha= ';ttl_02='º'; 
ttl_idx='num2str(alpha_values(idx))'; 
ttlOBJ='title(strcat(ttl_01,ttlIDX,ttl_02))'; 
%----
subplot(2,2,1)
plot(abs(Vdip(:,1)),abs(Ic1(:,1)),abs(Vdip(:,1)),abs(Ic2(:,1)),...
    abs(Vdip(:,1)),abs(Ic3(:,1)),abs(Vdip(:,1)),abs(Ic4(:,1)));grid on
idx=1; ttlIDX=eval(ttl_idx); eval(ttlOBJ);
eval(OBJ01); eval(OBJ02); eval(OBJ03);
lgOBJ=eval(obj_); eval(OBJ06); eval(OBJ07);
xlim([xo_lim xe_lim]); ylim([0 10.9]); 
%---
subplot(2,2,2)
plot(abs(Vdip(:,2)),abs(Ic1(:,2)),abs(Vdip(:,2)),abs(Ic2(:,2)),...
    abs(Vdip(:,2)),abs(Ic3(:,2)),abs(Vdip(:,2)),abs(Ic4(:,2)));grid
idx=2; ttlIDX=eval(ttl_idx); eval(ttlOBJ);
eval(OBJ01); eval(OBJ02); eval(OBJ03);
lgOBJ=eval(obj_); eval(OBJ06); eval(OBJ07);
xlim([xo_lim xe_lim]); ylim([0 10.9]); 
%---
subplot(2,2,3)
plot(abs(Vdip(:,3)),abs(Ic1(:,3)),abs(Vdip(:,3)),abs(Ic2(:,3)),...
    abs(Vdip(:,3)),abs(Ic3(:,3)),abs(Vdip(:,3)),abs(Ic4(:,3)));grid
idx=3; ttlIDX=eval(ttl_idx); eval(ttlOBJ);
eval(OBJ01); eval(OBJ02); eval(OBJ03);
lgOBJ=eval(obj_); eval(OBJ06); eval(OBJ07);
xlim([xo_lim xe_lim]); ylim([0 10.9]); 
%---
subplot(2,2,4)
plot(abs(Vdip(:,4)),abs(Ic1(:,4)),abs(Vdip(:,4)),abs(Ic2(:,4)),...
    abs(Vdip(:,4)),abs(Ic3(:,4)),abs(Vdip(:,4)),abs(Ic4(:,4)));grid
idx=4; ttlIDX=eval(ttl_idx); eval(ttlOBJ);
eval(OBJ01); eval(OBJ02); eval(OBJ03);
lgOBJ=eval(obj_); eval(OBJ06); eval(OBJ07);
xlim([xo_lim xe_lim]); ylim([0 10.9]); 

... COMENTADO PARA USARLO SOLO SI SE NECESITA
%print -dpdf  'D:\VirtualBox\Latex\Reportes\dfig\StatCom\fig\Paper080411_fig10.pdf'  
set(gcf,'PaperUnits','centimeters', 'papersize',[ancho altura],'paperposition', [0 0 ancho altura])
nmfig=[newDIR,nmFIG01];  print(gcf, '-deps', nmfig);

%print -dpdf Intensidad_sag_ang.pdf;  pause(1); clf; close;
%winopen  'Intensidad_sag_ang.pdf'
%print -depsc Intensidad_sag_ang.eps; % pause(1); clf; close;
%winopen  'Intensidad_sag_ang.eps'
%copyfile('Intensidad_sag_ang.eps',destine)
%pause(2); close all;
%}

%lgOBJ=eval(obj_); eval(OBJ06); eval(OBJ07);

%% Print
set(gcf,'PaperUnits','centimeters','PaperOrientation','landscape',...
    'PaperType', 'A5');
pprsz=get(gcf, 'PaperSize');
[wdth hght]=deal(20,14.5);
[lft,bttm]=deal((pprsz(1)-wdth)/2,(pprsz(2)-hght)/2);
set(gcf,'PaperPosition',[lft,bttm,wdth,hght])
print -dpdf 'test01.pdf'; pause(2);% clf; close;
winopen('test01.pdf')


```



{% include links.html %}
