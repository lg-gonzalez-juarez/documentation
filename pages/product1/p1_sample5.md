---
title: Electronics
keywords: sample
summary: "This is just a sample topic..."
sidebar: product1_sidebar
permalink: p1_sample5.html
folder: product1
---

## Sample Content


dir

```md
D:\wk_matlab\uc3m\mt\pc104\Matlab\ElctPtc\inversor\inversor3ph
```


## STATCOM, ODE solver

dir=`D:\wk_matlab\uc3m\mt\pc103\MTLB\CTR\solveODE`

```matlab
clear all; close all; clc

Vll=30; fnom=50;  d.L=10e-3;       d.R=3.5;
Udc=300;
%% valores a por unidad
Vbase=Vll*sqrt(2/3);  
ibase=2*sqrt(2);      
Sbase=(3/2)*ibase*Vbase;  
%Zbase=Vbase/ibase; Lbase=Zbase/wbase; Cbase=1/(Zbase*wbase);
d.wbase=2*pi*fnom; 
S=complex(5e1,2e1);  U=complex(30*sqrt(2/3),0); 
I=(2/3)*conj(S/U);   id0=real(I); iq0=imag(I); 

%% usando ODE
%%
tspan=[0 0.2];	Xo=[id0 iq0];  
Dd=0.01 ;  Dq=0;  Vd=300*Dd; Vq=300*Dq;
dVd=real(U)-Vd ,   dVq=imag(U)-Vq

%id=x(1), iq=x(2)
%fA=inline('[(d.L*d.wbase*x(2) - d.R*x(1) + dVd )/d.L ;(-d.L*d.wbase*x(1)- d.R*x(2) + dVq )/d.L]');
%invtrSMALLsgn=@(t,x)[fA];

invtrSMALLsgn=@(t,x)...
		[(d.L*d.wbase*x(2) - d.R*x(1) + dVd )/d.L;...
		 (-d.L*d.wbase*x(1)- d.R*x(2) + dVq )/d.L];

[t,y]=ode45(invtrSMALLsgn, tspan, Xo);
iDQ0=y(end,:), plot(t,y);
pause(2); close all
```

### Repaso de control

dir=`D:\wk_matlab\uc3m\mt\pc103\MTLB\CTR\Xian`


### Análisis de la respuesta del sistema de control

dir=`D:\wk_matlab\uc3m\mt\pc103\MTLB\statcom\dgrmBLCK` 

{% include links.html %}
