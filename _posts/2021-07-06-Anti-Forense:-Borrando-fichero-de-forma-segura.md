---
layout: post
title:  "Anti-Forense: Borrando ficheros de forma segura"
tags: Anonimato, Opsec, Metadatos
by: Andrew
---

![preview](https://i.ibb.co/TL3VZDQ/DELETE.png)

Que tal a tod@s, en este topics vamos a aprender los métodos antiforense utilizados por Hackers
paranoicos para borrar sus ficheros, todos los pasos y técnicas fueron probado en BackBox (sistema basado en Ubuntu)
los métodos son técnicamente efectivos, por lo tanto ten precaucionon de lo que borras.

##¿Por que borrar nuestros ficheros de forma segura?

Cuando hacemos Click derecho y borrar en realidad lo que estamos haciendo es esconder el contenido donde
no lo podamos ver, imagina una fiesta con invitados, en la fiesta están todos los invitados de la lista pero
el organizador de la fiesta quiere eliminar a un invitado así que borra el nombre de la persona a la cual quiere
eliminar y da por echo que el invitado ya no esta, pues imagina que nuestros ficheros son borrados solo del indice
y no asi del todo.

Hay métodos tanto por Hardware como por Software para la recuperación de los datos de un dispositivo
los cuales son efectivos a la hora de recuperar los datos que no han sido borrados de forma segura.

##Herramientas

Las herramientas que vamos a usar son los siguientes: **shred, wipe y mat**.

- shred : Es una herramienta la cual fue programada para borrar y sobrescribir ficheros
		  haciéndolos totalmente irrecuperables.

- wipe: Es una herramienta igual que shred, pero la única diferencia es que su máxima 
	    característica es la de borrar discos o cualquier otro medio de almacenamientos 
	   	externo o interno de forma segura y completa.

- Mat: Es una herramienta la cual tiene como función borrar los metadatos de ficheros 	
	   de forma rápida y segura.

En las distros de Kali y parrot (no se en las demás) wipe viene instalado por defecto y si no me equivoco mat
también viene instalado, pero de igual forma he aquí los comandos para instalar las herramientas que utilizaremos…


###shred

```sudo apt install shred```

###wipe

```sudo apt install wipe```

###mat

```sudo apt install mat```

##Usando shred

Shred es una de las herramientas que uso casi a diario para borrar logs y ficheros de todo tipo, shred
es recomendable usarlo para este propósito.

###Borrando un fichero individual:

```shred -v -z -n 10 -u imagen.jpg```

![preview](https://i.ibb.co/JKkkZ1p/Captura-de-pantalla-2021-08-02-00-16-32.png)


vamos a listar las opciones que hemos introducido…

-v : Ver el proceso de borrado
-z : Sobreescribir de ceros el fichero
-n : Numero de pasadas (por default de 4, lo recomendable es 30 a 40)
-u : Una vez sobreescrito borrar el fichero

###Borrando listado de ficheros:

Ahora vamos a borrar un listado de ficheros en formato jpg, seria las mismas opciones pero le pasamos
como parámetro el asterisco seguido de un punto y el nombre del formato de los ficheros ejemplo.

```shred -v -z -n 10 -u *.jpg```

##Usando wipe borrando particiones y dispositivo USB

Aunque wipe nos sirve para borrar ficheros individuales como lo hace shred, su máxima cualidad es la de
formatear un partición del disco o borrar de forma segura cualquier dispositivo de almacenamiento externo
pero antes vamos a borrar ficheros individuales.

###Borrando un solo fichero de forma rápida usando 4 pasadas:

```wipe -qfi 1627911080147.jpg```

###Borrando un solo fichero indicando el numero de pasadas en este caso vamos a eliminarlo 10 veces:

```wipe -qfi -Q 10 1627912127302.jpg```

###Borrando datos de dispositivos extraibles:

```wipe -kq /dev/hda3```

###Borrar todo el contenido de un directorio:
```wipe -rfi midirectorio/*```

#Borrando metadatos de ficheros

##¿Que son los metadatos?

Dejemos que te lo explique la wikipedia…

>La definición más concreta de los metadatos es qué son “datos acerca de los datos” y sirven para
suministrar información sobre los datos producidos. Los metadatos consisten en información que
caracteriza datos, describen el contenido, calidad, condiciones, historia, disponibilidad y otras
características de los datos.

Los metadatos están en prácticamente todo los ficheros que usamos a diario como ser imágenes PNG
y JPG en formatos de videos y documentos WORD, etc.

Los metadatos los cuales pueden delatarnos o matar nuestro anonimato se encuentran en ficheros de
formato: JPG, DOCX, PDF, ODT, ODX, XLSX, estos documentos pueden contener nombre de usuario, version
del sistema operativo y en el caso de las imágenes JPG estas pueden contener informacion de geolocalizacion
de donde fue tomada la fotografia, claro si el teléfono o cámara activo el GPS antes de tomar la fotografia.

##Usando MAT (Metadata Anonymisation Toolkit)

MAT es una herramienta de anonimizacion de metadatos, con esta herramienta podemos borrar los metadatos

###Listando los formatos soportados por mat
```mat -l <fichero>```

###Visualizando metadatos del fichero 
```mat -d <fichero>```

###Borrando metadatos
```mat <fichero>```

**Mat también cuenta con una interface grafica muy fácil de usar puede invocarla con el comando**

```mat-gui```

![preview](https://i.ibb.co/C25W4yT/Captura-de-pantalla-2021-08-02-22-09-43.png)

Tambien es posible falsificar los metadatos de un fichero con algunas herramientas entre la que mas destaca
es **exiftool**, pero ese es otro tema.

**FUENTES:**
-https://www.geoidep.gob.pe/conoce-las-id...os%20datos.
-https://en.wikipedia.org/wiki/Data_recovery
