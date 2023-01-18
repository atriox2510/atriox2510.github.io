---
title: Windows Exploit Suggester (python2) - Arreglar error "xlrd.biffh.XLRDError Excel xlsx file; not supported"
author: Atriox Banished
date: 2022-08-25
categories: [Bugs, Errores, Configuración, Python, Linux]
tags: [bugs, errores, configuración, python2, linux, pip2]
pin: true
---

## ¿Qué es Windows Exploit Suggester?
Es una herramienta que compara los niveles de parches de un objetivo windows con la base de datos de vulnerabilidades de Microsoft para detectar posibles parches faltantes en el objetivo. También notifica al usuario si hay exploits públicos y módulos Metasploit disponibles para los boletines que faltan.

Esta herramienta está desarrollada en python2 y se encuentra en el repositorio de Github de [AonCyberLabs](https://github.com/AonCyberLabs/Windows-Exploit-Suggester). Las dependencias, es decir, las librerías que utiliza esta herramienta son muy especificas en cuamto a su versión, sin embargo, el repositorio no lo especifica.

### Error 1 - Default python
Python 3.10 es la versión estable actual (proximamente 3.11). Entre python2 y python3 cambiaron varias cosas, entre ellas el nombre de librerias y demás. Al estar desarrollada con python2, al querer ejecutar el script haciendo `./windows-exploit-suggester.py` el SO detectará la versión instalada de python, sin embargo, si tanto python2 como python3 están disponibles, tomará python3 para ejecutar el script por lo que nos dará un error.
![](/assets/img/windows-exploit-suggester/error-1.jpeg)

Esto es facil de arreglar definiendo bien el shebang, es decir, la primera linea que especifica el lenguaje del script `#!/usr/bin/env python`. Solo hay que agregar un **2** al **python**.
![](/assets/img/windows-exploit-suggester/fix-1.jpeg)

### Error 2 - xlrd.biffh.XLRDError: Excel xlsx file; not supported
Este error se ocasiona debido a la versión de la librería xlrd, si solo ejecutamos `pip2 install xlrd` se instalará la ultima versión de esta librería.
![](/assets/img/windows-exploit-suggester/error-2.jpeg)

Sin embargo, la version **1.2.0** y anteriores, son compatibles con esta herramienta, por lo que es mejor ejecutar `pip2 install xlrd==1.2.0`.
![](/assets/img/windows-exploit-suggester/fix-2.jpeg)

Existe una versión de python3 de esta herramienta en el repositorio de Github de [Pwnistry](https://github.com/Pwnistry/Windows-Exploit-Suggester-python3). Recomendada para evitar estos problemas.

## REREFENCIAS
* Blog hablando de [Windows Exploit Suggester](https://blog.gdssecurity.com/labs/2014/7/11/introducing-windows-exploit-suggester.html)
* [Repositorio de la herramienta python2](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
* [Repositorio de la herramienta python3](https://github.com/Pwnistry/Windows-Exploit-Suggester-python3)
* [Post original de la resolución del problema](https://stackoverflow.com/questions/65254535/xlrd-biffh-xlrderror-excel-xlsx-file-not-supported)

## APOYO
* Sigueme en mi [Perfil de GitHub](https://github.com/atriox2510).
