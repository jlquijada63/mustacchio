
Descripcion de la maquina:

Se trata de una maquina con un servidor web vulnerable a la que se accede a traves de una vulnerabilidad XEE (XML External Entity). Para la escalada de privilegios se aprovecha una vulnerabilidad tipo SUID

Enumeracion de la maquina:

Puerto 22: ssh
Puerto 80: http (servidor apache)
Puerto 8765: http (servidor nginx) -> vulnerabilidad XEE

Penetraccion

En el servidor nginx (p:8765) hay un directorio /auth que contiene un archivo "dontforget.bak" donde se establece el formato del payload XEE que hay que enviar a traves de un formulario con una caja de texto que pide un comentario en XML

¿Que es XEE (XML External Entity)?
Algunos servidores web tienen entradas de datos en forma de campos de texto que exigen introducir los datos en formato XML. Estos servidores son vulnerables porque existe un elemento en XML llamado Entity que puede ser sustituido por cualquier cosa incluso por un ejejecutable:

		<!DOCTYPE foo [ 
			<!ENTITY xee SYSTEM "file:///path_of_file">
			]
			<name>jose</name>
			<apellido>perez</apellido>

Entity puede sustituir a cualquier elemento del XML:

En esta maquina a traves de esta tecnica podemos acceder a ficheros criticos como /etc/passwd o /.ssh/id_rsa

si conseguimos id_rsa de algun usuario, podremos acceder a la maquina consiguiendo el primer objetivo

el password el usuario (barry) es (urieljames)
