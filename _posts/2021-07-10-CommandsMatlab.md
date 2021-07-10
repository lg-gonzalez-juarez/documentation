---
title:  "Comandos Matlab"
categories: jekyll update
permalink: CommandsMatlab.html
tags: [news]
---

### Print Screen
```cmd
fprint-sprintf
```
<code>


## Setting Screen
```cmd
set(0,'units','centimeters')
get(0,'MonitorPosition')
get(0,'ScreenSize')
fprintf(lineSec,'a','Nombre Bloques');
disp(blks); pause (2); 
```

## Display properties of Simulink Blocks
```cmd
 for n=1:length(Tag_blck),  
    title=strcat(Tag_blck{n},'=> ',num2str(blks_pos{n}));
    fprintf('%s \n',title);
end

Position==[left bottom width height]; 
sprintf('%c',char(245)); tic
```

```cmd
U=1*exp(2*i*pi*50); 
    disp('U'); 
I=0.5*exp(-i*2*pi*50); 
    disp ('I')
S=U*conj(I); toc ; tic; 
    fprintf('%d \n',S); toc; tic; disp (S); toc
```

## no imprime variables
tic; sprintf('%d \n',S) ;toc


## Mejor opcion para desplegar lineas 

```cmd
tic; fprintf('%c',char(frame01));
fprintf('\n'); 
sprintf('%c',char(frame01)),sprintf('\n');toc

### Adaptacion de pc/folder en matlab

```cmd
addpath('D:\MTLB\bin\MyComputePrg\Sags'); 
addpath('D:\MTLB\bin\MyComputePrg\sourceVabc'); 
addpath(genpath('D:\THESIS\CODE\Matlab\sysREE\rev1'))
```

### SIZE SCREEN 

```cmd
scrsz = get(0,'ScreenSize'); en pixeles
... tipo centimeter normalized
left=1; bottom=1; width=20;  height=10; 
figure('units','centimeter','Position',[left, bottom, width, height]);

OTHERS
get(gcf,'Position');
set(gcf,'Units','centimeters');
```

### CONOCER EL TAMAÑO DE CADA MONITOR

```cmd
get(0,'MonitorPosition')
```

### Para imprimir al tamaño deseado

```cmd
set(gcf, 'PaperUnits', 'centimeters');
width = 15;   height = 15;        
set(gcf, 'PaperSize', [width height]);
papersize = get(gcf, 'PaperSize');       
left = (papersize(1)- width)/2;        
bottom = (papersize(2)- height)/2;       
myfiguresize = [left, bottom, width, height];        
set(gcf, 'PaperPosition', myfiguresize);
```

### Para imprimir al tamaño deseado

```cmd
set(gcf, 'PaperUnits', 'centimeters');
width = 15;   height = 15; 
set(gcf, 'PaperSize', [width height]);
papersize = get(gcf, 'PaperSize');
left = (papersize(1)- width)/2;
bottom = (papersize(2)- height)/2;
myfiguresize = [left, bottom, width, height];
set(gcf, 'PaperPosition', myfiguresize);
set(gcf,'Units','centimeters','Position',[4,14,15,10]);
set(gcf, 'PaperUnits', 'centimeters','PaperSize',[15,10],...
'PaperPosition',[0,0,15,10]);
```


PLOTS
```cmd
%print -dpdf Intensidad_sag_ang.pdf;  pause(1); clf; close;
%winopen  'Intensidad_sag_ang.pdf'
%print -depsc Intensidad_sag_ang.eps; % pause(1); clf; close;
winopen  'Intensidad_sag_ang.eps'     
%copyfile('Intensidad_sag_ang.eps',destine)
    pause(2); close all;
```

### Para ponerle nombre a una figura
```cmd
  
  figure('name','Ic-Vdip <-> Angulo de carga variando'); hold on
    %set(figH,'Name','something else','NumberTitle','off') 
```cmd
  
    Esto es la mejor opcion en tiempo de computo<code>
```cmd
    tic;disp(sprintf('%c',char(frame01)));toc
```
    
    
    datos de numero a letras
```cmd
    num2str(SG1(1:3,1)
```cmd
    
    formato pdf: existen 2 formas  a) usando un comando de linea, pero habria que darle el tamaño especifico  b) imprimiendo en eps y pasandolo a pdf usando un archivo en ubuntu para esta conversion <strong>formato eps:</strong><code>print -deps NameFile</code> <strong>Formato de impresion</strong><code>pdf o eps</code> <!-- --> 
    

### CONFIGURATION PLOTS:
    
```cmd
    iLocLeg='EastOutside'; ColorLine=[0 0 0]; StyleLine='.-|--|-.|:';  
    set(gcf,'DefaultLineLineWidth',1.5) set(gcf,'DefaultAxesColorOrder',ColorLine,...       
    'DefaultAxesLineStyleOrder',StyleLine)  
    iFontSize=14; iLineWidth=2; jFontSize=15; strFontName='Arial';
    set(gcf,'Defaultaxesfontsize',jFontSize,...     
    'DefaultAxesFontName','strFontName',... 'DefaultAxesFontUnits','centimeters');  
    %---PutNameAxes OBJ01='xlabel(strXlabel);ylabel(strYlabel)'; 
    %---PutSize/Type_Letter_atLATEX prop01='FontSize'; prop02='Interpreter'; INprop02='latex'; propA='XLabel'; propB='YLabel'; OBJ02='set(get(gca,propA),prop01,iFontSize,prop02,INprop02)'; OBJ03='set(get(gca,propB),prop01,iFontSize,prop02,INprop02)';  %----
```
    
### Colocar legendas en graficas

```cmd
     OBJ05='legend(strLegend)'; propE='type';  
     propF='text'; OBJ06='set(findobj(lgOBJ,propE,propF),prop01,jFontSize,prop02,INprop02)';
```
### Color y localizacion de las etiquetas

```cmd
     propG='boxoff'; propH='Location'; propI='edgecolor'; propJ='none';
     OBJ07='legend(propG,propH,iLocLeg,propI,propJ)'
     [num, txt, raw] = xlsread('CASOIIF.XLS') 
     wnd=num(:,1);
     windFILTER
     figure(1);
     rng default;%x=ecg(500)'+0.25*randn(500,1); 
     
     %noisy waveform     %{ 
     xWND=[wnd;wnd] h=fdesign.lowpass('Fp,Fst,Ap,Ast',0.15,0.2,1,60);
     d=design(h,'equiripple'); 
     %LowpassFIRFILTER 
     WNDfltr01=filtfilt(d.Numerator,1,xWND);
     %zero-phaseFILTER WNDfltr02=filter(d.Numerator,1,xWND);
     %conventionalFILTER  subplot(321);
     plot([WNDfltr01 WNDfltr02]);
     title('señales filtradas');
     legend('FILTRADO FASE-CERO','FILTRADO TRADICIONAL');%} 
     xWND=[wnd];  %subplot(211);  
     h=fdesign.lowpass('N,F3dB',12,0.15);  
     d1=design(h,'butter'); 
     WNDfltr03=filtfilt(d1.sosMatrix,d1.ScaleValues,xWND);  
     strYlabel='\bf{Viento (Medidas) [m/s]}'; 
     strXlabel='\bf{Tiempo [horas]}'; 
     strLegend={'Medici\''on sin tratar','se\~nal filtrada'};  
     %plot(tm,P1_24hrs,'og',tm,P2_24hrs,'sr',tm,P3_24hrs,'^b',tm,P4_24hrs,'*k'); 
     plot(xWND,'k-.'); hold on; plot(WNDfltr03,'r','linewidth',2); 
     %legend('MEDICION SIN TRATAR','SEÑAL FILTRADA','location','NorthEast'); 
     cy = get(gca,'xtick');  
     %set(gca,'xticklabel',[]); 
     set(gca,'xticklabel',cy/10);  
     eval(OBJ01); eval(OBJ02); eval(OBJ03); lgOBJ=eval(OBJ05);  eval(OBJ06);  eval(OBJ07); 
     axis([0 240 7.5 12.5]);grid on  
     %PRINT set(gcf,'PaperUnits','centimeters','PaperOrientation','landscape',...     
     'PaperType', 'A5'); pprsz=get(gcf, 'PaperSize'); 
     [wdth hght]=deal(20,14.5); 
     [lft,bttm]=deal((pprsz(1)-wdth)/2,(pprsz(2)-hght)/2); 
     set(gcf,'PaperPosition',[lft,bttm,wdth,hght])  
     nmFL='filtradoWND.pdf'; print('-dpdf',nmFL); 
     winopen(nmFL)
```

### Para saber que formato utilizar para desplegar datos por pantalla u archivo 

http://www.mathworks.es/help/techdoc/ref/fprintf.html 
     

### Exportar a latex
http://www.mathworks.es/help/techdoc/matlab_env/f6-30186.html


### Tipos lineas
```cmd
     --: trazado lineal discontinuo 
     g: verde oscuro (green)  
     -.: trazado lineal discontinuo intercalando punto y línea 
     k: negro (black)  
     : : trazado con línea de puntos 
     m: rojo oscuro (magenta) 
     *: marca * r: rojo (red) 
     +: marca 
     + w: blanco (white) 
     o: círculo 
     y: amarillo (yellow) 
     x: marca con un aspa 
     .: un punto 
     b: azul (blue) 
     c: verde claro (cyan  '-^b' '-.r' 
```

### Tipo de Datos
    A) ACCESO DATOS 
    1) cell       koman2:  NameCell{n_cell}  
    2) Numeric Arrays       
    koman2:  NameCell{n_cell} B = [12, 62, 93, -8, 22; 16, 2, 87, 43, 91; -4, 17, -72, 95, 6]  
    2) Character Strings myString = 'Hello, world';  
    
    A) ADMINISTRACION DATOS 
    1) Importación Datos   load: Números separados por espacios-> matriz  Puede cargar desde ficheros .mat o ASCII  
    load ('fichero .mat' [, var1, var2, varN ])  
    load('fichero ascii') %carga matrix de números  
    
    csvread → Hojas de cálculo        
    dlmread → Números, cualquier separador  t
    extread → para leer celdas, varios tipos   
    textscan → Más complejo y potente que textread  
    xmlread → Formatos XML → Document ObjectModel  Exportación de datos  
    save: Guarda datos para ser cargados con load  
    save ('fichero', variables...)  csvwrite  
    dlmwrite → Números, cualquier separador  
    xmlwrite → Guarda en formato XML 
    
    Uso general de ficheros
    1.Abrir: fopen 
    2.Lectura y escritura: fload, fwrite, fread, fscanf, fprintf... 
    3.Cerrar: fclose, Hay que comprobar posibles errores al operar con ficheros  
    Alternativas: Matlab(simple) y estilo C (potente)  
    [fid, msg]=fopen('nombre', 'modo') 
    -Modo: 
    - 'r' → fichero existente para lectura 
    - 'w' → escritura, borra el contenido previo 
    - 'a' → escritura, añadiendo al final del fichero 
    - 'r+' → fichero existente, lectura y escritura 
    - 'w+' → lectura y escritura, borrando el contenidoprevio 
    - 'a+' → lectura y escritura, al final del fichero   
    fprintf(fid, 'formato', variables...) 
    - Escribe las variables en el fichero siguendo el formato indicado 
    - Si se omite fid escribe en pantalla 
    - Formato: cadena de conversión estilo 
    C - %d %i: Decimal con signo - %o %u, %x: octal, sin signo, hexadecimal, 
    - %E,e: Double precisión, notación [-]d.ddddE(+|-)dd 
    - %f: [-]ddd.ddd; %g: usa %e o %f según el caso 
    - %s: cadena de caracteres Lectura y escritura 
    - Longitud y decimales: %l.d antes del modificador 
    - Delimitadores - \n: salto de linea - \r: retorno de carro 
    - \t: tabulador - \b: retroceso (backspace) 
    - \\: para imprimir \ (carácter de escape)  Lectura 
    - A= fscanf (fid, 'formato') -v=fscanf(fid, '%g') → Lee todo el fichero, numero a numero, volcandolo en el vector v 
    - [A, leidos] = fscanf(fid, 'formato', dimension) 
    - Leidos= leidos correctamente - Dimension 
    - n= n elementos en un vector columna 
    - inf=todos los elementos 
    - [M, N] Rellena la matriz MxN por columnas. N puede ser inf Lectura por lineas linea=fgetl(fid) → lee linea a linea (sin guardar \n). 
    -1 si llega al final de fichero (se puede comprobar con ~ischar(linea) 
    - fgets(fid) → lee la siguiente linea, incluyendo \n 
    - fgets(fid, nchar) → lee nchar caracteres máximo de la siguiente linea  
    
    Formato de numeros Orden de MATLAB Comentarios Ejemplo 
    format long  format short 16 dígitos  visualización por defecto 35.83333333333334  35.8333 
    format short e 5 dígitos más exponente 3.5833e+01 
    format long e 16 dígitos más exponente 3.583333333333334e+01 
    format hex hexadecimal 4041eaaaaaaaaaab 
    format bank 2 decimales 35.83 format + signo + format rat aproximación racional 215/6  
    
    La orden digits(n)cambia el número de dígitos de precisión que se usa por defecto en la toolbox.  
    La orden digits nos permite conocer cual es el valor de este número.  
    La orden vpapermite realizar un cálculo y mostrar su resultado con una precisión especificada  sin cambiar el número de dígitos de precisión con el que se trabaja por defecto.  
    source "http://www.nebrija.es/~mjgarbayo/seminario_matlab/matlab2.html" 
    
   ### Matlab to latex
   
   %url=http://pundit.pratt.duke.edu/piki/index.php?title=MATLAB:LaTeX_Table_Writer&oldid=9734 
    
   ```cmd
    s = sym(L);  
    v = vpa(s,5); 
    # assign numerical precision  
    latex(v)             
    TC = [-273.15 -40 0 100]';   
    TK = TC + 273.15;             
    TF = (TC+40)*9/5-40;             
    TR = TF + 459.67;              
    for k=1:length(TC)                 
    fprintf('%8.2f & %8.2f & %8.2f & %8.2f \\\\ \n', TC(k), TK(k), TF(k), TR(k))             
    end                          
    for k=1:length(TC)                 
    fprintf('%8.2f & %8.2f & %8.2f & %8.2f \\\\ \\hline  \n', TC(k), TK(k), TF(k), TR(k))             
    end                          
    
    FID = fopen('file.tex', 'w')             
    for k=1:size(MainMat, 1)                 
    fprintf(FID, '%8.2f & %8.2f & %8.2f & %8.2f \\\\ \n', TC(k), TK(k), TF(k), TR(k))             
    end             
    fclose(FID)                          
    
    FID = fopen('file.tex', 'w');             
    fprintf(FID, '\\begin{tabular}{|rrrr|}\\hline \n');             
    fprintf(FID, 'T ($^{\\circ}$C) & T (K) & T ($^{\\circ}$F) & T ($^{\\circ}$R)\\\\ \\hline \n');             
    
    for k=1:length(TC)                 
    fprintf(FID, '%8.2f & %8.2f & %8.2f & %8.2f \\\\ ', TC(k), TK(k), TF(k), TR(k));                 
    if k==length(TC)                     
    fprintf(FID, '\\hline ');                 
    end                 
    fprintf(FID, '\n');             
    end                           
    fprintf(FID, '\\end{tabular}\n');             
    fclose(FID);  %\begin{center} %\input{file.tex} %\end{center} 
   ```
    
   ## CONFIGURACION EDITOR
    
    El tipo de letra para el editor: consolas Colores para el Editor 
    Azul -> RGB[0,255,204]  %Azul muy padre tirando pa verde :-D tipos de verdes       
    verde-amarillo [189 221 150]       
    verde-azul-suave [130,239,178]        
    codigo ascii de caracteres utiles       
    0xAE -- flecha       U+219 --- Flecha okis       para saber el # ascii       
    clc;for n=126:1:255;disp([char(n) num2str(n)]);end 
    
    Customer fonts  toNUMBERS- muy visible: Dialog MS reference Sans 
    Serif palatino Linotype Miriam FIxed  Lucida Compacta: Iskoola Pota       

###    Coordenadas Polares

%PolarCoordinates 
```cmd
    angTHT= 0:0.01:2*pi; 
    rdR = sin(2*angTHT).*cos(2*angTHT); 
    [xX,yY]=pol2cart(angTHT,rdR); 
    figure;plot(xX,yY) 
    figure; polar(angTHT,rho,'--r')
```    
    
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
     
### to set ubuntu: transforn toeps desde 104 desde otro pc 

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
    
    
### Multiples salidas matlab
    para sacar muchos datos de otra funcion

```cmd 
    function[varargout]=ComputePointEq(sys,u_r0,u_s_eq,P_eq,Q_eq,varargin) 
    options=optimset('Display','off'); 
    %Solve system of nonlinear equations 
    u_r_eq=fsolve(@(u_r)kk(u_r,sys,u_s_eq,P_eq,Q_eq),u_r0,options);  
    u=[u_s_eq;u_r_eq];  
    x_eq=(eye(4)-sys.A)\(sys.B*u); 
    varargout{1}=u_r_eq; 
    varargout{2}=x_eq; 
    end
```
    
### LoadDatas
    
    Para cuando leemos los datos a partir de un file*.mat 

```cmd    
    nmFL='datas.mat'; load(nmFL) 
    vars1=whos('-file',nmFL) 
    load(nmFL,vars1.name)
    %d=load('nmFL','-regexp','x0',) 
    dato=importdata(nmFL) %dato.Y.Data %-- dato.X.Data --time %-- dato.Y.Name -- Esto esta padre pa saber que es cada dato nmDATA=dato.Y(1).Name,  
    subplot(211); 
    plot(dato.X.Data,dato.Y(4).Data,dato.X.Data,dato.Y(5).Data); 
    legend('Pmed','Pref') subplot(212); 
    plot(dato.X.Data,dato.Y(6).Data,dato.X.Data,dato.Y(7).Data); 
    legend('Qmed','Qref') 
```

### reducir NumDatos 
    Util para cuando tienes medidas

```cmd
    tic %--- reduciendo datos       
    Y1=output_discreto(:,1);       
    Y2=output_discreto(:,2);       
    U1=input_discreto(:,1);       
    U2=input_discreto(:,2);       
    n=3;       
    for i=1:1:n           
        Y1(1:2:end,:)=[];           
        Y2(1:2:end,:)=[];           
        U1(1:2:end,:)=[];           
        U2(1:2:end,:)=[];           
        t_stm(1:2:end,:)=[]; 
    end 
```

    info matlab web;       
    http://www.mathworks.es/help/techdoc/ref/f16-42340.html#f16-6755     
    http://www.mathworks.es/help/techdoc/ref/f16-42340.html
    
    ### Conocer las propiedades de un objeto

```cmd 
    whos objeto, 
    whos T5_par
    string => character array <!-- -->  
```
        
    ### PROGRAMACION BASICA
    listfonts 
    
    FNCanonimous
    http://blogs.mathworks.com/loren/2013/01/10/introduction-to-functional-programming-with-anonymous-functions-part-1/ 
    
```cmd 
    c=@(a, b, theta)
    sqrt(a.^2+b.^2-2*a.*b.*cos(theta)) 
    MaxMin=@(x) [min(x), max(x)];  
    MaxMin(2) ans =     2     2 
    [extremo,idx] = cellfun(@(f) 
    f([3 4 1 6 2]), {@min, @max}) 
    min_and_max = @(x) 
    cellfun(@(f) f(x), 
    {@min, @max}); 
    y = randi(10, 1, 10) 
    
    just_values  = min_and_max(y) 
    [~, just_indices]  = min_and_max(y) 
    [extrema, indices] = min_and_max(y) 
    mapc = @(val, fcns) 
    cellfun(@(f) f(val{:}), fcns, 'UniformOutput', false); mapc({pi}, {@(x) 2 * x, ...  
    % Multiply by 2             @cos, ...
    % Find cosine             @(x) sprintf('x is %.5f...', x)})   
    % Return a string MIO: mapc=@(val,fcns) cellfun(@(f) f(val{:}),fcns,'UniformOutput',false); oxx=mapc({230}, {@(x)x*sqrt(2/3),@cos,@(x) sprintf('x is %.5f...', x)})   </code>  
```    
    
### Integrales 
    http://www.cs.cmu.edu/~tom/10601_fall2012/recitations/matlab_quickref.pdf 
    
    ### Inline function
```cmd
    f1=inline(’1./(2*x.^3-2*x-5)’); 
```

```cmd    
    Q=quad(f1,0,2); f2=@(x)1./(2*x.^3-2*x-5);Q=quad(f2,0,2);</code> <!--  --> <b>Edit Folders, Filese</b><!--  --> <code>movefile('source','destination')</code> <!--  --> <b> function symbolicas</b> si se usa una funcion simbolica se puede  substituir valor con <b>subs </b>
```

     <hr><b>STRINGS</b><!--  --> a = 'hello  ';      b = 'goodbye';     using_strcat = strcat(a, b)     using_arrayop = [a, b]      % Equivalent to horzcat(a, b)      
    
    MATLAB returns     
    using_strcat =hellogoodbye     
    using_arrayop =hello  goodbye     
    alfabeto griego en latex para matlab
    
    
     <!--  --> <b>String Evaluation</b>  <code>eval, feval</code> <b>multiplicacion matrices</b> <code>clear all; close all; clc %% multiplicacion Matrix %a(mn) syms a11 a12 a13 %a11...a1n syms a21 a22 a23  syms a31 a32 a33 %am1..anm %b(np) syms b11  %b11...b1p syms b21   syms b31  %bn1..anp  A=[a11,a12,a13;... a21,a22,a23;... a31,a32,a33]; %am1..anm B=[b11;b21;b31]; C=A*B </code> 
    
    <!--  --> <hr><b> MATRIX</b> Para sumar los elementos de una matrix <code>  [baseMVA, bus, gen, branch] = loadcase(casefile);     % obtener el vector de las potencias      P=bus(:,3);    Q=bus(:,4);     PQ=bus([1:4],[3 4]) %submatrix elementos donde se interseptan filas 1,4  y columnas 3,4     % en la primera prueba usamos todas la potencias para que sea la total     Pt_test1=sum(P,1) % 1 es para que sume en vertical     Qt_test1=sum(Q,1)% 1 es para que sume en vertical     PQ_1=sum(PQ,1)     % en la segunda prueba solo emplearemos las 3 primeras cargas     PQ_tst2=bus([1:3],[3 4])%submatrix elementos donde se interseptan filas 1,3  y columnas 3,4     PQ_2=sum(PQ_tst2,1)       source:algabra matlab</code>  <!--  -->    
    
    
    <hr><b>VECTORES</b>
    dot-product of two vectors -- norm(V) cross computes the cross product of two vectors in R3.
    
    
    <hr><caption> ATAJOS KOman2</caption>  
    
    Para seleccionar matlab con el tabulador   para seleccionar en la barra superior Alt+ F E V b D W H <!--  --> <b> abrir archivos de un pc remoto:</b><code>strcat(old_dir,'\',NameFile)</code>  $ en el path colocar &lt;- \tsclient\D) <!--  -->   
    
    <hr><caption> FOLDERs</caption> 
    <b>MOVER ARCHIVO AL FOLDER CHILDREN </b>  
    
    carpeta destino   
```cmd
    NameFolderChildren='sub01'   
    copyfile('source','destination')     
    NameFolderChildren='sub01'    
    NameFile='dt_2G_8buses.m'           
    source=strcat(old_dir,'\',NameFile)           
    destino=strcat(old_dir,'\',NameFolderChildren,'\',NameFile)
    copyfile(source,destino)
```

### MOVER FILE
```cmd
    NameFile='datos_fglongatt.m'   
    source=strcat(old_dir,'\',NameFile)   
    destino=strcat(old_dir,'\',NameFolderChildren,'\',NameFile)   movefile(source,destino) </code> <!--  -->     <hr><b>abrir archivos de un pc remoto:</b> function anonymous:   A = [2 3 4];<br>B = [5 6 7];       sumAxBy = @(x, y) (A*x + B*y);       sumAxBy(5, 7) <!--  -->  Code performance  checkcode('filename')  Inilation variables  function q = fcnPersist1(u) % fcnPersistent creates and uses a       persistent variable. persistent y; <br> if isempty(y),    y = u;<br> else,    y = y+1;<br> end q = y;)  <!-- <br>  -->  <hr><b>FOR-CICLOS: </b>          <tt> syms a11 a12 b21 b22              A=[a11;a12];              B=[b21;b22];             % mover               for i=1:1:2;               for j=1:1:2;              fprintf('i=%d j=%d \n',i,j)                C(i,j)=A(i)
    *B(j);              fprintf('Matrix C \n');               disp(C); pause(1)             end           end </tt>  <!--  -->  

```

    <hr><b>MOVE folder:</b> $para mover un archivo a un children_folder       
    &lt;- algun comentario necesario<!-- --> <!--  -->    
    
    <b>INDICAR DIRECCION ACTUAL</b> old_dir=pwd;  B=[b21;b22];<!--  -->           
    
    
    
    <b>CARPETA DESTINO</b><!-- --> <code>NameFolderChildren='sub01'        copyfile('source','destination')       NameFolderChildren='sub01';       NameFile='dt_2G_8buses.m'       source=strcat(old_dir,'\',NameFile)       destino=strcat       (old_dir,'\',NameFolderChildren,'\',NameFile)       copyfile(source,destino)