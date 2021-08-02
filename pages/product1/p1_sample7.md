---
title: Filtros
keywords: sample
summary: "En este apartado se presentan varios ejemplos de matlab enfocados al diseño de filtros"
sidebar: product1_sidebar
permalink: p1_sample7.html
folder: product1
---

## Directorios

`D:\wk_matlab\uc3m\mt\pc103\MTLB\CTR\procSGN`

```matlab
d = fdesign.lowpass('Fp,Fst,Ap,Ast',1e3,1100,0.5,60,1e4);
Hd = design(d);
fvtool(Hd)

%Use filter() to apply your filter to the data:
%output = filter(Hd,input);

disp('================')

%%
%link=http://stackoverflow.com/questions/15110458/low-pass-filtering-not-working-as-expected


Fs = 1000;                    % Sampling frequency
T = 1/Fs;    % Sample time
L = 1000;                     % Length of signal
t =(0:L-1)*T;                % Time vector 
x = 0.7*sin(2*pi*50*t) + sin(2*pi*120*t);  % Sum of a 50 Hz sinusoid and a 120 Hz sinusoid %
y = x + 2*randn(size(t));     % Sinusoids plus noise

y = x ;

figure('name','Signal')
plot(Fs*t(1:50),y(1:50));title('Signal');xlabel('time (milliseconds)')

%pause;
NFFT = 2^nextpow2(L); % Next power of 2 from length of y
Y = fft(y,NFFT)/L; f = Fs/2*linspace(0,1,NFFT/2+1);

% Plot single-sided amplitude spectrum.
figure('name','amplitude spectrum')
plot(f,2*abs(Y(1:NFFT/2+1))) 
title('Single-Sided Amplitude Spectrum of y(t)');xlabel('Frequency(Hz)');ylabel('|Y(f)|')

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%       Now let us see Low Pass Filtering of this signal  
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

Fp= (2*pi * 30)/1000; %=0.184 %only frequncies less than 30Hz will be passed  

%d=fdesign.lowpass('Fp,Fst,Ap,Ast',0.184,0.185,2,60);
%d=fdesign.lowpass('Fp,Fst,Ap,Ast', 2*30/Fs, 2*35/Fs,2,60);

d=fdesign.lowpass('Fp,Fst,Ap,Ast', 30, 35,2,60, Fs);

designmethods(d);

Hd = design(d,'equiripple'); fvtool(Hd);

Filterd_Output = filter(Hd,y);

NFFT = 2^nextpow2(L); % Next power of 2 from length of y
Filtered_Freq = fft(Filterd_Output,NFFT)/L;
f = Fs/2*linspace(0,1,NFFT/2+1);
```


{% include links.html %}
