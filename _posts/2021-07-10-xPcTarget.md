---
title:  "xPcTarget"
categories: jekyll update
permalink: xPcTarget.html
tags: [news]
---

## xPcTarget

La compatibilidad de matlab se tiene hasta 2011, con respecto al código realizado en phD.


### Puntos a considerar antes de comenzar a trabajar con xPcTarget

Durante el arranque del xpc target es necesario generar un disco de arranque del pc maestro. Este disco después se emplea como disco de arranque del pc esclavo. También es necesario comprobar el correcto funcionamiento de el compilador de matlab. Revisar tener instalada la versión estable en el momento de usar xPcTarget

## Ecuaciones de estado

Metodo.  obteniendo ecuaciones de estado espacio
... Para obtener the state-space representation of the model circuitl with the power_analyze command.

```cmd
%sys1 = power_analyze('Dstatcom_v1','structure')
sys1 = power_analyze('Dstatcom_v2','structure') %sps = power_analyze('Dstatcom_v1','sort')
```

## Notitas de control
Una interrupcion del bobinado de excitacion durante el funcionamiento en vacio de un motor de continua en derivacion trae por consecuencia que el motor se desboque.

# Procedimiento del uso de xPcTarget con la tarjeta de labview

## Pasos de configuración y puesta en marcha de un xPc-Target

1. Encender el XPC target (el blanco).

2. Ejecutar Matlab

3. Con el comando ``xpctargetping`` conoces el  estado de operación, el despliege en pantalla del mensaje ``success`` indica la correcta operación de la xPcTarget.  

4. Para conocer los detalles de la xPCtarget``getxpcenv``

5. Para configurar la xPCtarget ``xpcexplr``. En esta pantalla se observan los osciloscopio del host

6. Para conocer las características de las tarjetas que tienes en la xPCtarget  se usa el comando [getxpcpci]. Aparece en pantalla el listado de dispositivos PCI conectados asi como sus principales caracteristicas útiles para el procesado de datos:

```cmd
National Instruments     PCI-6025E
     Bus 0, Slot 11, IRQ 12
     AI AO DI DO Counter
     VendorID 0x1093, DeviceID 0x2a80

National Instruments     PCI-6040E (PCI-MIO-16E-4)
     Bus 0, Slot 13, IRQ 11
     AI AO DI DO Counter
     VendorID 0x1093, DeviceID 0x1190
```

En este ejemplo se emplea el dispositivo ``PCI-6040E``

**NOTA:** solo se usan la primera vez que se configura la xPCtarget

7. En el archivo con extensión “mdl”, insertas los bloques entrada y salida de la tarjeta de adauisicion.
8. Las funciones para la tarjeta están el toolbox “xPCTarget”
9. La adquisición de datos se hace con: xPCtarget => A/D  =>  National Instruments => PCI6040E.
10. La configuración de la entrada del bloque (SLOT13)
11. Para el PWM se emplea:  xPCtarget => counter  =>  National Instruments => PCI6040E Generate
12. Para configurar durante operación ejecute el comando ``xpcexplr``

## Hackings

En la tabla de esta sección se resumen comandos útiles en el desarrollo de sistemas de control implementados en la xPCTarget:

| Command |Description|
|xpctest| executes a test suite to check for proper setup of the xPC Target environment|
|xpctargetping|ping's the actual xPC target computer and returns either `success` or `failed`|
|getxpcpci| queries the target PC for installed PCI devices (boards) and displays information about the found PCI devices in the command window|
|rtwintgt|Install and remove the Real-Time Windows Target kernel|