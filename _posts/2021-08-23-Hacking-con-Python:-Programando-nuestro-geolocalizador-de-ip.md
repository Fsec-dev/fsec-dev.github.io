---
layout: post
title:  "Python Hacking: Programando nuestro geolocalizador de IP"
tags: Programacion, Python
by: Andrew
---

Que tal este es el primer Topic de una serie de Topic ligado al Hacking
usando Python, en estas series compartire pequeños Topics con codigos para
desarrollar tus Scripts y usarlo en tu dia a dia.

En esta ocasion vamos a programar nuestro pequeño Script el cual nos sera
util para obtener la ubicacion del servidor de la url o ip que le pasemos
como parametro a nuestro Script.

Todos los Scripts que programemos en estas series se lo hara usando Python3
por lo tanto toma encuenta usar Python3.

## Herramientas necesarias:

- **Un editor de codigo (se recomienda SublimeText o Visual Code)**
- **Python3 instalado en tu sistema**
- **Conexion a internet**

## Comencemos

Para este Script vamos a usar el modulo **Requests** el cual si no lo
tienes instalado en tu sistema puedes instalarlo con el siguiente comando
```pip3 install requests``` esta libreria nos sera util para interactuar
con servidores Web, en este caso para interactuar con el servidor ipinfo.io
esta pagina nos permite hacer consultas sobre alguna ip y nos lanza los resultados
en formato json (es un formato de texto sencillo para el intercambio de datos)
y otras de las ventajas de este formato es que se puede parsear y analizar
de forma facil los datos.

Para parsear los datos devuelto por el servidor nosotros vamos a usar el
modulo de Python3 llamado **json** no necesitas instalarlo, este ya viene
por default en Python3, y por ultimo vamos a importar el modulo **sys** y **socket**
para que nuestro Script reciba parametros en este caso la Ip que le indiquemos y
el modulo socket convertir las urls en ips.

por lo tanto empezemos importando los modulos necesarios...

```python

import sys
import json
import socket
import requests

UA = "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.9 Safari/537.36"
```

Luego creamos una variable con un diccionario dentro, el cual va hacer el User-Agent
que vamos a usar para hacer las consultas al servidor de infoip, tu puedes obtener
el User-agent de cualquier otro navegador, pero en mi caso voy a usar el user agent de 
Chrome sobre una maquina Windows **(Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.9 Safari/537.36)**
este user agent lo obtuve gracias al complemento para firefox **User-Agent Spoofer** o puedes obtener
otro buscando en internet.

Creamos la estructura basica de un Script en Python...

```python
def main(host)
	#...
	
if __name__ == "__main__":
	#...
```

Vamos a escribir primero dentro del **if**, en esta parte vamos a obtener los parametros que 
le pasemos al Script como ser la URL o una IP, tambien vamos a verficar el parametro que le pasemos
en caso de ser una URL eliminar el nombre del protocolo (http/https) y solo quedarnos con la direccion
por ejemplo, ingresamos https://website.com  y solo nos quedariamos con website.com, ya que mas adelante
solo vamos a usar la direccion sin el http.

```python
if __name__ == "__main__":
	if len(sys.argv) < 2:
		print ("\nGeoIp 0.1v - 2021")
		print ("\n{} <ip/url>\n".format(sys.argv[0]))
	else:
		target = sys.argv[1]

		if target.startswith("http"):
			target = target.split('/')[2]

		main(target)
```

Pasemos a la funcion principal la cual se encargara de realizar toda la operacion que nos interesa
Esta funcion recibira la ip o url para luego realizar la consulta a ipinfo.io el servidor nos 
devolvera toda la informacion en formato Json la cual nos sera facil parsear gracias al modulo Json

```python
def main(host):

	host = socket.gethostbyname(host)

	url = "https://ipinfo.io/"+host+"/json"
	r = requests.get(url, headers=UA)
	
	if r.status_code != 200:
			print ("\nError {}\n".format(r.status_code))
	else:
		j = json.loads(r.text)

		ip = j['ip']
		country = j['country']
		city = j['city']
		region = j['region']
		geo = j['loc']
		isp = j['org']
		timezone = j['timezone']
		
		print ("""
GEOIP Version 0.1v

IP: {}
Pais: {}
Ciudad: {}
Region: {}
Geolocalizacion: {}
ISP: {}
Zona Horaria: {}
		""".format(ip, country, city, region, geo, isp, timezone))
```
## Demo:
<img src="https://i.ibb.co/R3R7Kfn/geoip-capture.png">

Listo ya tienes tu pequeña herramienta de geoip lista y funcional, si deseas
usarla desde cualquier parte desde tu terminal puedes copiar el Script a la ruta
**/sbin** con el siguiente comando... ```cp script.py /sbin/``` ahora ya tienes
tu pequeña herramienta.

**Script completo:** https://github.com/Fsec-dev/Cursos_Python/blob/main/geoip.py

**Bye and Happy Hacking**
