---
layout: post
title:  "Protegiendo Payload de cierres de procesos"
tags: Post-explotation  Metasploit Hacking
---

Que tal chic@s, hoy vengo a mostrarles una técnica muy útil en nuestra fase de Post Explotacion, vamos a proteger nuestro pequeño
ejecutable de cualquier técnica de cierre, convirtiéndolo en un dolor de cabeza para el administrador del ordenador victima, esta
técnica puede ser usada tanto en ordenadores Windows de 32 y 64 bits.

Bueno, nos vamos a Github y descargamos este modulo para metasploit (https://github.com/EgeBalci/MSF-Self-Defense/) pero espera...vamos
a guardarlo en la siguiente ruta (/opt/metasploit-framework/embedded/framework/modules/post/windows/manage), para luego alojar el fichero
self_defense.rb (ruby) en ese directorio, listo ya estamos listo para usarlo en nuestros ataques.

## USO:

Este modulo es un modulo de post explotacion, lo que quiere decir que vamos a usarlo en una session meterprete iniciada, para este topic
yo tengo una session de un ordenador Windows de 32bits.

![preview](https://i.ibb.co/BVcmB5q/sessions.png)

**Ahora en metasploit invocamos nuestro modulo de la siguiente forma...**

![preview](https://i.ibb.co/RCb0dt8/self-defender-1.png)

`use post/windows/manage/self_defense`

He introducimos el id de nuestra session, en mi caso es 1 `set SESSION 1` ejecutamos con `run` y listo.

![preview](https://i.ibb.co/njsrT6B/self-defender-2.png)

## Ordenador victima

Ahora lo que pasaría en el ordenador victima seria que nuestro pequeño payload.exe no pueda ser cerrado, en mi caso el fichero malicioso se
llama darkarmy.exe.
![preview](https://i.ibb.co/k5gZ9nf/self-defender-3.png)

Como pueden ver, intento matar el proceso desde el administrador de tareas de Windows y me salta un error impidiéndome el cierre del proceso.
Luego intento un proceso mas agresivo desde la consola de windows (cmd.exe), con el comando `taskkill /F /IM darkarmy.exe /T` y me lanza un 
error de acceso denegado.

![preview](https://i.ibb.co/jb9jsSb/self-defender-4.png)

El Script fue escrito por EgeBalci un Hacker Turco, el cual tiene un Blog muy interesante con varios métodos de evasión. https://pentest.blog (En Ingles)
