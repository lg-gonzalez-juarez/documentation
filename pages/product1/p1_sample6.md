---
title: Control
keywords: sample
summary: "This is just a sample topic..."
sidebar: product1_sidebar
permalink: p1_sample6.html
folder: product1
---

## Comandos relativos a gráficos
`D:\wk_matlab\uc3m\mt\pc104\Matlab\basics\MyPlotsCurves`


## Comandos relativos a control

En este apartado se resumen los comandos para obtener los valores del controlador de tipo PID, basado en la función de transferencia de la planta a controlar

```md
D:\wk_matlab\uc3m\mt\pc104\MTLB\src\CTR\discrete
```

```matlab
%% diseño con comandos de matlab
clear all; close all; clc;

%% from:cascadepiddemo

d=struct('Sn',1.5e3,'fs',1e4,'Vd',230,'L',2e-3,'C',1100e-6,'R',3.5,'Vdc',1700);
[d.Ts,d.tau]=deal(1/d.fs,d.L/d.R);%pag19
d.T=d.Ts/2; d.Ti=d.tau; d.Kp=d.tau*d.R/(2*d.T);
d.Teq=2*d.T; d.a=2.41;
d.Tiv=d.a^2*d.Teq; 
d.Kpv=2*d.Vdc*d.C/(3*d.Vd*sqrt(d.Tiv*d.Teq));
sprintf('======== Data Estructura ============');
disp(d)

%% PLANT
G.plt.tf=tf(1,d.R*[1 d.R/d.L]);%[num,den]=tfdata(G.plt.tf,'V')
G.dly.tf=tf(1,[d.T 1]);
G.ctrI.tf=tf(d.Kp*[d.Ti 1],[d.Ti 0]);

F.plt.tf=tf(1,[d.C 0]);
F.ffw.k=1.5*(d.Vd/d.Vdc);
F.dly.tf=tf(1,[d.Teq 1]);
F.ctrU.n=d.Kpv*[d.Tiv 1]; F.ctrU.d=[d.Tiv 0]; F.ctrU.tf=tf(F.ctrU.n,F.ctrU.d);


sprintf('======== Planta OPEN LOOP ============');
P1 =G.plt.tf*G.dly.tf

bndWDTH=bandwidth(P1);
sprintf('bandwith: %.2f',bndWDTH)

figure('name','polos G_OL'),rlocus(P1); 

ppp=pole(P1)';
sprintf('polo: %.2f \n',ppp)

[Gm,Pm,Wcg,Wcp] = margin(P1);%Gm-GainMarrgen %PhaseMargin: Pm

fprintf('GM: %d \t crossover frequency (Wcg): %d \n',Gm,Wcg);
[CA InfoA] = pidtune(P1,'pi') 

C0 = pidstd(d.Kp,1,1,1,'InputName','e','OutputName','u');
C0

%discrete
%C0 = pidstd(1,1,1,1,'Ts',d.Ts,'IFormula','BackwardEuler',...
 %                            'DFormula','BackwardEuler');
%[CA infoA] = pidtune(c2d(P1,d.Ts),C0)
%[CA infoA] = pidtune(c2d(P1,1),C0)

```


```matlab
P2=F.plt.tf%*F.ffw.k*F.dly.tf;
[CB InfoB] = pidtune(P2,'pi') 

%% Designing a Single Loop Control System with a PI Controller
% The plant model is P = P1*P2
P = P1*P2;
[C Info] = pidtune(P,'pi') 
% Use a PID or PIDSTD object to define the desired controller structure
C = pidstd(1,1);
%wo=3e2;%1/(sqrt(2)*d.T)
%OPT = pidtuneOptions('Crossover',2*Info.CrossoverFrequency); 
wo=Info.CrossoverFrequency/2;
% Use pidtune options to specify performance and robustness targets
options = pidtuneOptions('CrossoverFrequency',wo*10);
% Design PI controller

C = pidtune(P,C,options);
sprintf('========\n'), disp(C)


%% Designing a Cascade Control System with Two PI Controller
C2 = pidtune(P2,pidstd(1,1),pidtuneOptions('CrossoverFrequency',wo));
C2

% Inner loop system when the control loop is closed first
clsys = feedback(P2*C2,1);
% Plant seen by the outer loop controller C1 is clsys*P1
C1 = pidtune(clsys*P1,pidstd(1,1),pidtuneOptions('CrossoverFrequency',wo*10));
C1

%% Performance Comparison
figure('name','Performance Comparison')
% single loop system for reference tracking
sys1=feedback(P*C,1); set(sys1,'Name','Single Loop');
% cascade system for reference tracking
sys2=feedback(clsys*P1*C1,1);set(sys2,'Name','Cascade');
% plot step response
subplot 211
step(sys1,'r',sys2,'b');
legend('show','location','southeast')
title('Reference Tracking')

% single loop system for rejecting d2
sysd1 = feedback(P1,P2*C); set(sysd1,'Name','Single Loop');
% cascade system for rejecting d2
sysd2 = P1/(1+P2*C2+P2*P1*C1*C2); set(sysd2,'Name','Cascade');
% plot step response
subplot 212
step(sysd1,'r',sysd2,'b');legend('show');title('Disturbance Rejection')

```

### Truquitos útiles

```cmd
D:\wk_matlab\uc3m\mt\pc104\MTLB\src\CTR\discrete
```

En formato simbolico

```matlab
clear all; close all;clc

fprintf('\n Simbolico')
Gp.sym=sym('1/(T*s+1)');
Gp.gt=ilaplace(Gp.sym);
Gp.gt=subs(Gp.gt,'t','k*Ts');
Gp.z1=ztrans(Gp.gt);
Gp.z=times(Gp.z1,'(z-1)/z');
Gp.Gz=collect(Gp.z,'z')
Gp.Gz=simplify(Gp.Gz)
disp('Funciones simbolicas')
[num,den]=numden(Gp.Gz)

num=subs(num, 'T',1.0);
den=subs(den, 'T',1.0);
num=subs(num, 'Ts',0.01);
den=subs(den, 'Ts',0.01);
numN=sym2poly(num), denN=sym2poly(den)
printsys(numN,denN,'z')
```

### Usando un modelo de matlab

```matlab
% use P controller with gain=1
[numcl,dencl]=feedback(numN,denN,1,1);
dstep(numcl,dencl)
xlabel('Time (k*0.1sec)')
ylabel(' ')
open_system('M1')
sim('M1')
```

### Método de discretización

```matlab
d.L=10e-3;d.R=3;
Gp.tfCNT=tf(1,[d.L/d.R 1])
Gp.Ts=1e-4;
Gp.tfDSC=c2d(Gp.tfCNT,1e-4,'zoh')
%[Gp.nmDSC,Gp.dnDSC]=tfdata(Gp.tfDSC,'v');
```

```matlab
fprintf('\n \tFuncion Transf. Planta con delay interno entrada');Gp.tf.cntDLYin
disp('discretizado');
Gp.tf.dscDLYin=c2d(Gp.tf.cntDLYin,Gp.Ts,'zoh');
Gp.tf.dscDLYin
```

#### Propiedades de la función de transferencia

```matlab
fprintf('\n Propiedades de los sistemas')
get(Gp.tfDSC),get(Gp.tf.dscDLYin)
```

```matlab
[Gp.nmDSC,Gp.dnDSC]=tfdata(Gp.tfDSC,'v');
fprintf('\n \tFuncion Transf. Planta'); 
printsys(Gp.nmCNT,Gp.dnCNT,'s')
printsys(Gp.nmDSC,Gp.dnDSC,'z')
%---
celldisp(get(Gp.tfDSC,'num')),
celldisp(get(Gp.tfDSC,'den'))

%% 
roots(Gp.dnCNT)
roots(Gp.dnDSC)
```

### Gráficas de la función de transferencia

```matlab
subplot 211, stepplot(Gp.tfCNT,Gp.tfDSC);
title('Respuesta al escalon lazon abierto')
GCL.cnt=feedback(Gp.tfCNT,1)
GCL.dsc=feedback(Gp.tfDSC,1)
subplot 212, stepplot(GCL.cnt,GCL.dsc)
title('Lazo Cerrado')
```

### Gráfica en lazo abierto

```matlab
%% PLANT with internal time Delays en la entrada
Gp.dlyIN=2;
Gp.tf.cntDLYin=tf(Gp.nmCNT,Gp.dnCNT,'InputDelay',Gp.dlyIN);%exp
fprintf('\n \tFuncion Transf. Planta con delay interno entrada');Gp.tf.cntDLYin
disp('discretizado');
Gp.tf.dscDLYin=c2d(Gp.tf.cntDLYin,Gp.Ts,'zoh');
Gp.tf.dscDLYin

%...PLANT with internal time Delays en la salida
%pltB=tf(1,[Ts 1],'OutputDelay',3,'Ts',0.001)
%---- planta actuador y sensor

str.Ttl.A='planta';
str.Ttl.B='planta con retraso';

subplot 211,step(Gp.tfCNT); hold on; step(Gp.tfDSC,'-or'); hold off;
title(str.Ttl.A); 
subplot 212,step(Gp.tf.cntDLYin); hold on; step(Gp.tf.dscDLYin,'-or'); hold off;title(str.Ttl.B); 
set(gcf,'PaperPositionMode','auto','units','pixels','Position',[1,53,1024,1150])

fprintf('\n Propiedades de los sistemas')
get(Gp.tfDSC),get(Gp.tf.dscDLYin)

%--
stpInfo.cnt = stepinfo(Gp.tfCNT)
stpInfo.dsc = stepinfo(Gp.tfDSC)
stpInfo.cntDLYin = stepinfo(Gp.tf.cntDLYin)
stpInfo.dscDLYin = stepinfo(Gp.tf.dscDLYin)

[x1,x2,x3,x4]=margin(Gp.tfCNT)
[y1,y2,y3,y4]=margin(Gp.tfDSC)
[z1,z2,z3,z4]=margin(Gp.tf.cntDLYin)
[r1,r2,r3,r4]=margin(Gp.tf.dscDLYin)


%% Closing Feedback Loops with Time Delays

%...REGULATOR
Gr.tfCNT=pid(0.5,2.3);
Gr.tfDSC=c2d(Gr.tfCNT,Gp.Ts,'zoh');
Gt.tf.cnt=feedback(Gr.tfCNT*Gp.tfCNT,1)
Gt.tf.cntDLYin=feedback(Gr.tfCNT*Gp.tf.cntDLYin,1)
```

### Gráficas en lazo cerrado

```matlab
%--planta+control en lazo cerrado
Gt.tf.dsc=feedback(Gr.tf.dsc*Gp.tf.dsc,1)
Gt.tf.dscDLYin=feedback(Gr.tf.dsc*Gp.tf.dscDLYin,1)

%-ForwardEuler-'zoh'
figure()
subplot 211;step(Gt.tf.cnt);hold on; step(Gt.tf.dsc);hold off
subplot 212;step(Gt.tf.cntDLYin);hold on; step(Gt.tf.dscDLYin);hold off

%{
G = tf(1,[1 10],'InputDelay',2.1);C = pid(0.5,2.3);
T = feedback(C*G,1);T.InternalDelay;step(T)
%}
 
disp('SMILE @@ ...... :-D')
figure()
P = bodeoptions('cstprefs')
P.PhaseUnits='rad';
P.PhaseMatching='on';
P.PhaseWrapping='off';
P.MagScale='linear';
P.PhaseMatchingFreq=3;
P.PhaseMatchingValue=2*pi;
h1=bodeplot(Gp.tf.cnt,P)
h2=getoptions(h1)

figure(); 
subplot 411,margin(Gp.tf.cnt);
subplot 412,margin(Gp.tf.dsc);
subplot 413,margin(Gp.tf.cntDLYin);
subplot 414,margin(Gp.tf.dscDLYin);

figure();
bodeplot(Gp.tf.cnt,Gp.tf.dsc,'or',Gp.tf.cntDLYin,Gp.tf.dscDLYin,'+m',P); 
legend('cnt','dsc','cntDLY','dscDLY')
title('planta')

figure()
bodeplot(Gt.tf.cnt,Gt.tf.dsc,'or',Gt.tf.cntDLYin,Gt.tf.dscDLYin,'+m',P); 
legend('cnt','dsc','cntDLY','dscDLY')

%ltiprops(Gt.tf.dscDLYin)
```


## Implementación del control vectorial 

`D:\wk_matlab\uc3m\mt\pc104\Matlab\basics\SpcVctr`

{% include links.html %}
