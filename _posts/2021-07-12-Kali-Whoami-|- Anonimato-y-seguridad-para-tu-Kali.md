---
layout: post
title: Kali-Whoami |  Anonimato y seguridad para tu Kali
tags: Opsec, Kali, Script
---

Que tal chic@s espero que se encuentren bien, y si no lo están tranquil@s que no hay mal que dure 100 años, todo en esta vida es posible
con algo de esfuerzo y dedicación.

Hoy les traigo una herramienta la cual me gusto bastante puesto que añade ciertas configuraciones a tu sistema para que puedas navegar
de forma anonima y hackear como un Ghost Hacker, que tal si empezamos... 

Kali hoy en día es un estándar como sistema operativo para Hackers, tanto novatos como expertos en el tema de Hacking usan este sistema
operativo, pero como saben Kali no trae las configuraciones necesarias para el bien de tu anonimato y privacidad, existen un montón de
técnicas para poder configurar tu OS para obtener anonimato y privacidad, también existen herramientas que automatizan esta tarea, una
de ellas es Kali-whoami.

## ¿Que es kali-whoami?

![preview](https://user-images.githubusercontent.com/59175356/124522019-530f3480-ddfa-11eb-8e8b-a678b01b9254.PNG)

Kali-whoami es una herramienta programada en Bash y Javascript fue creada para configurar tu sistema para que puedas obtener anonimato y
privacidad con ciertas configuraciones tanto en tu sistema como en el navegador Firefox, la herramienta te brinda una interface amigable
dentro de la terminal la cual te resultara imposible perderse.

## Instalacion

**Instalacion de los modulos nesesarios:**

```sudo apt update && sudo apt install tar tor curl python3 python3-scapy network-manager```

**Clonacion del repositorio:**

```git clone https://github.com/omer-dogan/kali-whoami```

**Instalacion del makefile**

```sudo make install```

### Instalacion desde un paquete deb

kali-whoami cuenta también con un paquete deb que puedes instalarlo fácilmente con una sola linea de comando…

```wget https://github.com/omer-dogan/kali-whoami/releases/download/v1.0/kali-whoami.deb && dpkg -i kali-whoami.deb```



## Como usarlo

La interface de kali-whoami es muy intuitiva no hay por donde perderse, lo que si tienes que saber son las opciones de seguridad 
que tiene, voy a enumerar las opciones que tiene esta herramienta para saber de que se tratan y que configuración hará en nuestro
sistema.

![preview](https://user-images.githubusercontent.com/59175356/124754970-cc8d4c80-def8-11eb-8606-02c6cdd7f5a2.gif)

### Opciones:

**Anti mitm:** Con esta opción activada nosotros estamos a salvo  de un ataque mitm, nuestra información que fluye por una red comprometida
no estará expuesta al atacante.

**Log Killer:** Los sistemas operativos recolectan información de forma local para que podamos ver como se comporta nuestro sistema o red, pero
esta información puede ser muy valiosa para un atacante externo o si eres un BlackHat Hacker esta información puede ser muy valiosa para los
analistas forenses, con esta opción borras los log que genera kali.

**IP changer:** Con esta opción torificas tu sistema kali haciendo que toda tu conexión TCP pase atravez de Tor.

**Dns Changer:** Puedes cambiar tu servidor DNS, esto te ayudara a que tu ISP no pueda ver por cuales sitios navegas.

**Mac changer:** Puedes cambiar tu dirección MAC para que dentro de una red no pueden determinar que tipo de ordenador posees (Hardware).

**Anti cold boot:** Un ataque de arranque en frío es un proceso para obtener acceso no autorizado a las claves de cifrado de una computadora
cuando la computadora se deja desatendida físicamente, con esto activado anulas este pido de ataque.

**Timezone changer:** Con esto cambias la hora de tu sistema y la zona horaria para que no puedan asociar la hora de tu sistema con la ubicación de tu pais.

**Hostname changer:**  cambias el nombre de tu sistema para que no puedan ver tu nombre de usuario.

**Browser anonymation:**  Añades ciertas configuraciones al navegador Firefox para que no puedas enviar información a los servicios web que visitas.

**Notas finales:** Yo en lo personal no uso Kali por lo tanto decidí probarlo en mi BackBox y me funciono muy bien, en el proyecto de github están trabajando
para hacerlo compatible a cualquier sistema Gnu/Linux.

**Github: https://github.com/omer-dogan/kali-whoami**

**Saludos y Happy Hacking!!**
