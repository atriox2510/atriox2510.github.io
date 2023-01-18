---
title: activeMon.sh - Scripting
author: Atriox Banished
date: 2022-07-03
categories: [Scripting, Bash, Linux]
tags: [scripting, bash, linux, ping, icmp]
---

Esta es una herramienta programada en bash, la cual nos permite monitorear si un host está activo o no a través de paquetes echo ICMP.

## PING
Es importante que el host el cual se monitorea acepte mensajes ICMP.
~~~bash
atriox@kali:~$ ping -c 1 127.0.0.1
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.228 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.228/0.228/0.228/0.000 ms
~~~

## CODIGOS DE ESTADO
Cuando se ejecuta exitosamente el ping, nos devuelve un código de estado es `extitoso=0`.
~~~bash
atriox@kali:~$ echo $?
0
~~~

Cuando falla, el código de estado es `erróneo=1`.
~~~bash
atriox@kali:~$ ping -c 1 12.0.0.12
PING 12.0.0.12 (12.0.0.12) 56(84) bytes of data.

--- 12.0.0.12 ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 0ms
atriox@kali:~$ echo $?
1
~~~

## ¿CÓMO FUNCIONA?
Para evitar que el script cree peticiones que se queden en espera durante mucho tiempo usaremos el tiempo de vida de comando en bash.
~~~bash
timeout 3 bash -c "ping -c 1 127.0.0.1"
~~~

Ahora si se ejecuta **exitosamente** el comando entonces se ejecutará también otra cosa, en este caso la palabra **_Activo_**.
~~~bash
&& echo "Activo"
~~~

Ahora si se ejecuta **erróneamente** el comando entonces se ejecutará otra cosa, en este caso la palabra **_No Activo_**.
~~~bash
|| echo "No Activo"
~~~

Para evitar ver en la consola mensajes de exito y error del ping, redirigimos estos al `/dev/null` y entre ping y ping, hay un descanso de 4 segundos de monitoreo.
~~~bash
timeout 3 bash -c "ping -c 1 $target" &>/dev/null
~~~

Ahora sí, ya tenemos todo para que funcione la herramienta. Para ejecutarla, pondremos lo siguiente.
~~~bash
wget https://raw.githubusercontent.com/atriox2510/activeMon/main/activeMon.sh
chmod +x activeMon.sh
./activeMon.sh 192.168.100.1
~~~

## DEMO
![](/assets/img/activeMon/demo.png)

## APOYO
Apóyame dándome una estrella en el repositorio de la herramienta en [GitHub](https://github.com/atriox2510/activeMon) y siguiéndome en mi [Perfil](https://github.com/atriox2510).
