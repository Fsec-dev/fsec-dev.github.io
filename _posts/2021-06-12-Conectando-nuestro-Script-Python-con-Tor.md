---
layout: post
title:  "Conectando nuestro Script Python con Tor"
tags: Programacion, Python, Tor
author: Andrew
---
![preview](https://i.ibb.co/2hmHfG7/file-1.jpg)

Que tal, en este pequeño articulo vamos a aprender a realizar consultas a sitios Web
con nuestros Scripts con Python pero de forma anónima, para este tutorial
vamos a utilizar las siguientes herramientas...

- **Python3**
- **Sublime Text u otro editor**
- **Tor**
- **Libreria Requests**
- **Un cerebro en buen estado**

Como dije anteriormente, vamos a necesitar de la librería requests para este tutorial
podemos instalarlo de la siguiente forma... `pip3 install requests` una vez instalado
proseguimos.

##Programming motherfuckers

Empezamos por la cabecera de nuestro Script, creamos el hashbag y le indicamos que
vamos a usar el interprete de Python 3, luego exportamos las librerias que vamos a usar
en este caso vamos a usar **sys** y **requests**.

```
#!/usr/bin/env python3

import sys
import requests
```

Ahora vamos crear la funcion mas importante de este tutorial, el cual se va a encargar de 
conectarnos con Tor, para esto vamos a hacer uso del metodo Session que nos brinda la 
libreria requests, con esto vamos a crear un proxy solo para usarlo con requests, son mas
palabras, vamos al codigo...

```
def session_tor():
    session = requests.session()
    # Por defecto el sock de Tor en Linux se mantiene en el puerto 9050
    session.proxies = {'http':'socks5h://127.0.0.1:9050',
                       'https':'socks5h://127.0.0.1:9050'}
    return session
```

Notaras que hemos introducido una IP local y el numero de puerto 9050 el cual
esta a la escucha por default en nuestro ordenador una vez instalado Tor.

![preview](https://i.ibb.co/KyKr3G2/tor-nmap.png)

Si tu no tienes el puerto abierto en tu sistema asegurate que tor esta corriendo
con el comando `service tor status` si vez que el servicio esta inactivo, puedes
usar el comando `service tor start` para levantar el servicio.

![preview](https://i.ibb.co/tKwL32R/tor-status.png)

## Poniendo a prueba el proxy

Es hora de poner a prueba nuestro proxy Tor, vamos a crear una funcion el cual tiene
como unica funcion devolvernos el header del servidor.

La funcion recibira como parametro la url a la cual nos conectaremos, luego adentro de
la funcion creamos una instancia llamada session, la cual usaremos para conectarnos al
servidor por medio de los nodos de Tor.

```
def consulta(host):
    session = session_tor()
    req = session.get(host, headers={'User-Agent':UA})

    if req.ok:
        for header in req.headers:
            print(header + " :" + req.headers[header])
    else:
        print (str(req.status_code))
```

## Codigo completo

```
#!/usr/bin/env python3
import sys
import requests

# Sock5 (Tor)
def session_tor():
    session = requests.session()
    # Por defecto el sock de Tor en Linux se mantiene en el puerto 9050
    session.proxies = {'http':'socks5h://127.0.0.1:9050',
                       'https':'socks5h://127.0.0.1:9050'}
    return session

def consulta(host):
    session = session_tor()
    req = session.get(host)

    if req.ok:
        for header in req.headers:
            print(header + " :" + req.headers[header])
    else:
        print (str(req.status_code))

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print ("USO: \n\n{} <host>\n".format(sys.argv[0]))
    else:
        consulta(sys.argv[1])
```

![preview](https://i.ibb.co/pLgWcL7/tor-request.png)

Apartir de aqui ya las posibilidades son muchas, puedes desarrollar 
un fuzzer dir para sitios onion, crear un Script para ataques de diccionarios
sobre paginas con login, etc.

Eso fue todo, Happy Hacking!!


**Fuentes: https://docs.python-requests.org/en/master/user/advanced/#proxies**
			
