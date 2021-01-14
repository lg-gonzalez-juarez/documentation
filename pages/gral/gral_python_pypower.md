---
title: Python Pypower
keywords: documentation, python, technical writers, help, authoring tools, replacements
last_updated: December 30th, 2020
tags: [formatting]
summary: Here documentation relative python
sidebar: general_sidebar
permalink: gral_python_pypower.html
folder: mydoc
output: web, pdf

---

## Pypower

### 1. Download the package Pypower

{% include callout.html content="First, download or clone the package from the [Github repo pypower](https://rwl.github.io/PYPOWER/). In Github, click the **Clone or download** button, and then click **Download ZIP**" type="info" %}

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i> download
<a alt='install process' href='https://pypi.org/project/PYPOWER/'>source code PyPower</a>
</div>

{% include tip.html content="For a better terminal emulator on Windows, use [Git Bash](https://git-for-windows.github.io/). Git Bash gives you Linux-like control on Windows." %}

### 2. Install Pypower

{% include important.html content="If you've never installed or run a PyPower site locally on your computer, follow these instructions to install PyPower: <a alt='install process' href='https://rwl.github.io/PYPOWER/install.html'>Install Pypower on Windows</a>., info." %}

code is the following:

```python
git clone http://github.com/rwl/PYPOWER.git
python setup.py installl
```
### 3. Commands
{% include note.html content=" 
More information above main commands of API PyPower are updated with the latest trends, best practices, and main methods on:"%}

* [Documentation about API](https://rwl.github.io/PYPOWER/api/) 
* [github-pages PyPower](https://rwl.github.io/PYPOWER/usage.html#application-programming-interface)

### usage
from https://pypi.org/project/PYPOWER/

to list the commands options
```python
pf h
```

PYPOWER includes a selection of test cases. For example, to run a power flow on the IEEE 14 bus test case:
```python
pf -c case14
```

The opf command has the same calling syntax. For example, to solve an OPF for the IEEE Reliability Test System and write the solved case to file:
```python
opf -c case24_ieee_rts --solvedcase=rtsout.py
```

### Command DC power flow
```python
import os
import sys
print(os.getcwd())
#cls
from pypower.api import case9, ppoption, rundcpf
ppc = case9()
ppopt = ppoption(PF_DC=True)
print("load case and execute dcpf")
ppc = case9()
r = rundcpf(ppc, ppopt)
```
#### Result

```python
Converged in 0.00 seconds
================================================================================
|     System Summary                                                           |
================================================================================

How many?                How much?              P (MW)            Q (MVAr)      
---------------------    -------------------  -------------  -----------------  
Buses              9     Total Gen Capacity     820.0           0.0 to 0.0      
Generators         3     On-line Capacity       820.0           0.0 to 0.0      
Committed Gens     3     Generation (actual)    314.0               0.0
Loads              3     Load                   315.0               0.0
  Fixed            3       Fixed                315.0               0.0
  Dispatchable     0       Dispatchable           0.0 of 0.0        0.0
Shunts             0     Shunt (inj)              0.0               0.0
Branches           9     Losses (I^2 * Z)         0.00              0.00
Transformers       0     Branch Charging (inj)     -                0.0
Inter-ties         0     Total Inter-tie Flow     0.0               0.0
Areas              1

                          Minimum                      Maximum
                 -------------------------  --------------------------------
Voltage Magnitude   1.000 p.u. @ bus 1          1.000 p.u. @ bus 1
Voltage Angle      -4.06 deg   @ bus 9          9.80 deg   @ bus 2

================================================================================
|     Bus Data                                                                 |
================================================================================
 Bus      Voltage          Generation             Load
  #   Mag(pu) Ang(deg)   P (MW)   Q (MVAr)   P (MW)   Q (MVAr)
----- ------- --------  --------  --------  --------  --------
    1  1.000    0.000*    66.00      0.00       -         -
    2  1.000    9.796    163.00      0.00       -         -
    3  1.000    5.061     85.00      0.00       -         -
    4  1.000   -2.211       -         -         -         -
    5  1.000   -3.738       -         -       90.00      0.00
    6  1.000    2.207       -         -         -         -
    7  1.000    0.822       -         -      100.00      0.00
    8  1.000    3.959       -         -         -         -
    9  1.000   -4.063       -         -      125.00      0.00
                        --------  --------  --------  --------
               Total:    314.00      0.00    315.00      0.00

================================================================================
|     Branch Data                                                              |
================================================================================
Brnch   From   To    From Bus Injection   To Bus Injection     Loss (I^2 * Z)
  #     Bus    Bus    P (MW)   Q (MVAr)   P (MW)   Q (MVAr)   P (MW)   Q (MVAr)
-----  -----  -----  --------  --------  --------  --------  --------  --------
   0      1      4     67.00      0.00    -67.00      0.00     0.000      0.00
   1      4      5     28.97      0.00    -28.97      0.00     0.000      0.00
   2      5      6    -61.03      0.00     61.03      0.00     0.000      0.00
   3      3      6     85.00      0.00    -85.00      0.00     0.000      0.00
   4      6      7     23.97      0.00    -23.97      0.00     0.000      0.00
   5      7      8    -76.03      0.00     76.03      0.00     0.000      0.00
   6      8      2   -163.00      0.00    163.00      0.00     0.000      0.00
   7      8      9     86.97      0.00    -86.97      0.00     0.000      0.00
   8      9      4    -38.03      0.00     38.03      0.00     0.000      0.00
                                                             --------  --------
                                                    Total:     0.000      0.00
```

{% include warning.html content="Es importante comprobar un consumo de potencia solo activa (MW)." %}

### links
* [MATPOWER from PSERC - Cornell](http://www.pserc.cornell.edu/matpower/)
* [MatDyn by Stijn Cole](http://www.esat.kuleuven.be/electa/teaching/matdyn/)
* [PSAT by Federico Milano](http://www.uclm.es/area/gsee/web/Federico/psat.htm)
* [OpenDSS from EPRI](http://sourceforge.net/projects/electricdss/)
* [GridLAB-D from PNNL](http://sourceforge.net/projects/gridlab-d/)
* [PyCIM](http://www.pycim.org/)

{% include links.html %}
