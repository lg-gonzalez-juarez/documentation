---
title: Electronics
keywords: sample
summary: "This is just a sample topic..."
sidebar: product1_sidebar
permalink: p1_sample5.html
folder: product1
---

## Sample Content

{% include callout.html content="**Code Repo** = D:\wk_matlab\uc3m\mt\pc104\Matlab\ElctPtc\inversor\inversor3ph" type="info" %}


## VSC & STATCOM,
Se resuelve en sistema en representación ODE definiendo el solver mas adecuado

{% include callout.html content="**Code Repo** = D:\wk_matlab\uc3m\mt\pc103\MTLB\CTR\solveODE" type="info" %}


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

{% include callout.html content="**Code Repo** = D:\wk_matlab\uc3m\mt\pc103\MTLB\CTR\Xian" type="info" %}


### Análisis de la respuesta del sistema de control

{% include callout.html content="**Code Repo** = D:\wk_matlab\uc3m\mt\pc103\MTLB\statcom\dgrmBLCK" type="info" %}


## Modelado & Setting completo

{% include callout.html content="**Code Repo** = D:\wk_matlab\uc3m\mt\pc104\Matlab\ElctPtc\MODELS_STATCOM_ck\KaiSimMdl" type="info" %}


```matlab
clear all; close all; clc

%% simbolicEQ
%{
syms L u R t w
%e=u+CUR*complex(R,L*w)
%w=sym('w(t)');tht=diff(w,t)
tht=int(w,t)
CUR=sym('CUR(t)')
euler=exp(-j*tht);
CUR=CUR*euler
U_L=L*diff(CUR,t)
U_R=CUR*R
Ug=u*exp(-j*tht)
break
%}

d=struct('R',24.8e-3,'L',2e-3,'w',100*pi);
s=tf('s');
[aD,aFF]=deal(d.L*s+d.R,d.L*d.w);
M=[aD,-aFF;aFF,aD];%M=[d.L*s+d.R,-d.L*d.w;d.L*d.w,d.L*s+d.R];
Madj=[aD aFF;-aFF aD];
detM=aD*aD-(-aFF*aFF);
invM=Madj/detM;

tf1=aD/detM;
tf2=aFF/detM;
G_jw=[0 tf(-aFF);tf(aFF) 0]

fprintf('\n*************************\n')
Gbis=minreal(invM/(1-(Madj*G_jw/detM)))

GJW=feedback(invM,G_jw,1)

t=0:0.1:10; dltU=-0.1*(t>4 & t<6);%disturbance
u=[ones(size(t));ones(size(t))];%u=[Vd;ones(size(t))];              
%lsimplot(GJW,u,t)

G=1/M; 
set(G,'InputName',{'id','iq'},'OutputName',{'Vd','Vq'},'variable','p');
fprintf('sysFT: Gzpk')

Gzpk=zpk(minreal(G));%Gzero=tzero(G);
Gss=ss(Gzpk);fprintf('sysSS: Gss')
[sysG1,g,T,Ti]=balreal(minreal(Gss))
%type='modal';%companion
%[G1,T]=canon(G,type);%balreal(G1)%minreal(G)
G2ss=ss2ss(sysG1,T)
%H=[0 -d.L*d.w;d.L*d.w 0];
Gdscpl=minreal(feedback(G,G_jw,1))

F=(d.R/d.L)*eye(2);
F=[0 -1;1 0]
G_=(1/d.L)*eye(2);
%dotX=

kFF1=1/dcgain(G(2,1)); kFF2=1/dcgain(G(1,2));
C1=tf(kFF1,[1 0]);     C2=tf(kFF2,[1 0]); 
kC=[0 kFF1;kFF2 0];    cl_ff=G_*kC

%'InputName',{'w_ref','Td'},'OutputName','w'
%set(cl_ff);

%title('Setpoint tracking and disturbance rejection')
% Annotate plot
%line([5,5],[.2,.3]); line([10,10],[.2,.3]);
%text(7.5,.25,{'disturbance','T_d = -0.1Nm'},...
 %           'vertic','middle','horiz','center','color','r');
    
%% FEEDBACKctr
%rlocusplot
Grlc=Gdscpl;
sysRLCS=tf(1,[1 0])*Grlc(1,1);
[R,K] = rlocus(sysRLCS)


TFp=tf(1,[1 d.L/d.R]);
[R,K] = rlocus(tf(1,[1 0])*TFp)
for idx=1:1:length(K)%-13
%KK=K(10);
KK=K(idx)
CC=tf(KK,[1 0])
GCL=feedback(CC*TFp,1)
%rlocusplot(GCL); hold on
stepplot(GCL);hold on 
end

ctrC=append(CC,CC)
figure();G_FB=feedback(ctrC*Grlc,1,1,1);
step(G_FB,2);

%figure();lsimplot(cl_ff,G_FB,u,t);
%set(G_FB,'InputName',{'uq','ud'},'OutputName',{'id','iq'});
%title('Setpoint tracking and disturbance rejection')
%legend('feedforward','feedback w/ rlocus','Location','NorthWest')

figure();bodeplot(cl_ff,G_FB)
```
## Bibliografia: 

- [ ] Kai tesis dinamarca
- [ ] TFM Linda & Barrado


## Modelo promediado

dir
`D:\wk_matlab\uc3m\mt\pc104\MTLB\src\ElctPtc\MODELS_STATCOM_ck\statcomFiltro`



