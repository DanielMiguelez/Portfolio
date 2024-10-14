# Proceso de instalación de Apache en Ubuntu

A continuación, describo los pasos que seguí para instalar el servidor web Apache en mi sistema operativo Ubuntu. Incluyo capturas de pantalla que muestran el proceso en detalle.

## 1. Actualización de los repositorios

Lo primero que hice fue actualizar la lista de repositorios en mi sistema para asegurarme de que todas las versiones estuvieran al día. Ejecuté el siguiente comando en la terminal:


### sudo apt update

Una vez actualizado el sistema, procedi a instalar apache usando el comando apt:

### sudo apt install apache2

Este proceso tardó unos minutos, ya que descargó y configuró los archivos necesarios para el servidor web.

Después de la instalación, verifiqué que Apache estuviera funcionando correctamente. Utilicé el siguiente comando para comprobar su estado:

### sudo systemctl status apache2

El estado indicó que Apache estaba activo y ejecutándose sin problemas.


Para confirmar que Apache estaba instalado correctamente, abrí un navegador web y escribí la dirección http://localhost. Esto me mostró la página predeterminada de Apache, lo cual confirmó que el servidor estaba funcionando.

### sudo ufw allow 'Apache Full'

verifiqué los cambios con el comando:

### sudo ufw status

Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Apache                     ALLOW       Anywhere                
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Apache (v6)                ALLOW       Anywhere (v6)


COmprobamos si se encuentra en ejecucion: 

### sudo systemctl status apache2

Obtener la dirección IP del servidor

Finalmente, utilicé el siguiente comando para obtener la dirección IP de mi servidor. Esta dirección es útil para acceder al servidor Apache desde otros dispositivos en la red:

### hostname -I


# CREACION DE UNA VIRTUALBOX PROPIA

Repaso paso a paso de todo el proceso de crear una virtual box, con todos los comandos utilizados mas imagenes del proceso.

1. Verificar la versión de Apache instalada

Primero, intenté verificar la versión de Apache con el comando:

### APACHE2 -V

Sin embargo, obtuve un error, ya que el comando está mal escrito (debe estar en minúsculas). Así que lo corregí y ejecuté:

### apache2 -v

El resultado mostró que tenía instalada la versión Apache/2.4.41 (Ubuntu), confirmando que Apache estaba correctamente instalado en mi sistema.

2. Crear el directorio del sitio web

Luego, decidí crear un directorio para mi nuevo sitio web en /var/www/. Utilicé el siguiente comando para crear un directorio llamado gci:

### sudo mkdir /var/www/gci/

Después de ingresar mi contraseña de usuario, el directorio se creó sin problemas.

3. Crear el archivo index.html

Me moví al nuevo directorio que acabo de crear:

### cd /var/www/gci/

Intenté crear un archivo index.html utilizando el comando cd seguido de nano index.html, lo que generó un error porque no estaba usando el comando de manera correcta. Así que volví a intentarlo con:

### nano index.html

No obstante, tuve que usar permisos de administrador, por lo que finalmente ejecuté:

### sudo nano index.html

Esto me permitió abrir el editor nano y comenzar a crear el archivo index.html con el contenido que quise añadir para mi sitio web.

4. Crear un archivo de configuración del sitio

Después, accedí al directorio de configuración de Apache, ubicado en /etc/apache2/sites-available/:

### cd /etc/apache2/sites-available/

Allí, copié el archivo de configuración por defecto de Apache (000-default.conf) para crear uno nuevo para mi sitio llamado gci:

### sudo cp 000-default.conf gci.conf

Luego, edité este nuevo archivo de configuración con:

### sudo nano gci.conf

5. Habilitar el nuevo sitio en Apache

Después de crear y editar el archivo de configuración, lo habilité para que Apache lo reconociera como un sitio activo. Inicialmente, cometí un error al escribir el comando SUDO A2ENSITE GCI.CONF en mayúsculas, lo que generó un error. La forma correcta es:

### sudo a2ensite gci.conf

Este comando habilitó el sitio web, y Apache me indicó que debía recargar la configuración para aplicar los cambios:

### service apache2 reload

6. Editar el archivo /etc/hosts

Después de habilitar el sitio, necesitaba asociar el nombre de dominio local (gci.example.com) con la dirección IP en mi sistema. Para esto, edité el archivo /etc/hosts:

### sudo nano /etc/hosts

En este archivo, agregué la siguiente línea para asociar mi dominio local con la dirección IP 127.0.0.1:

### 127.0.0.1	gci.example.com

Guardé los cambios y verifiqué que el contenido del archivo estuviera correcto usando:

### cat /etc/hosts

Este comando mostró las entradas correctas, y mi archivo /etc/hosts quedó configurado para permitir que el dominio gci.example.com se resuelva localmente en mi servidor.
7. Comprobación final

Por último, realicé una comprobación para asegurarme de que todo estuviera en orden, usando:

### sudo systemctl status apache2

Este comando me mostró que Apache estaba en ejecución. También utilicé el comando:

### hostname -I

Este me devolvió la dirección IP de mi servidor, confirmando que Apache estaba correctamente configurado y en funcionamiento.

De esta manera, logré configurar Apache con mi propio sitio local llamado gci en Ubuntu.

