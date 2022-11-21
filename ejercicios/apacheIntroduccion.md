# Instalación y configuración de apache
>Por Sergio Azogue  

En este archivo veremos como instalar apache y configurarlo para que podamos acceder a nuestro servidor con la dirección que nosotros le indiquemos en la configuración desde el terminal de ubuntu.

## Introducción  
La instalación se llevará a cabo en un equipo con un sistema Ubuntu 20.04. Instalaremos Apache, un software de servidor web HTTP con el que podremos alojar nuestra web. Es el más usado del mundo. Una alternativa podría ser miniweb.  
  
Apache nos servirá para hacer de nuestro equipo un servidor y poder configurarlo en base a nuestras necesidades. Podremos insertar páginas webs y acceder a estas mediante la ip de nuestro equipo.  
Empezaremos con la actualización de paquetes locales:  
```
sudo apt update
```  
Y luego instalaremos el paquete Apache2:
```
sudo apt install apache2
```  
Antes de empezar con apache debemos ajustar el firewall para permitir el acceso externo. Para ello primero listaremos los perfiles de aplicación ufw:  
```
sudo ufw app list
```  
Devolvería algo así:
```
Aplicaciones disponibles:  
Apache
Apache Full
Apache Secure
CUPS
```  
Habilitaremos el perfil:  
```
sudo ufw allow 'Apache'
```  
En mi caso tenía el firewall inactivo, con lo que en ese caso deberiamos activarlo con el siguiente comando:  
```
sudo ufw enable
```  
Una vez ya activo podremos ver la lista:  
```
sudo ufw status
```  
Ahora comprobaremos si el servicio se está ejecutando:  
```
sudo systemctl status apache2
```  
Otra forma de comprobarlo es poniendo la ip del servidor en el navegador. Para conocer la ip usaremos el siguiente comando:  
```
hostname -I
```  
Poniendo la ip en el navegador nos saldrá la siguiente ventana:  
![](https://assets.digitalocean.com/articles/how-to-install-lamp-ubuntu-16/small_apache_default.png)  
Una vez listo el servidor usaremos algunos comandos básicos de administración:  
Para detener el servidor usaremos el siguiente comando:  
```
sudo systemctl stop apache2
```  
Para iniciarlo estando inactivo:  
```
sudo systemctl start apache2
```  
Para reiniciarlo:  
```
sudo systemctl restart apache2
```  
Para recargar sin cerrar la conexión:  
```
sudo systemctl reload apache2
```  
Por defecto cuando se inicia el equipo se iniciará el servidor. Para deshabilitar este comportamiento deberá usar el siguiente comando:  
```
sudo systemctl disable apache2
```  
Y para volver a habilitarlo:  
```
sudo systemctl enable apache2
```  
## Configuración  
  
Para poder acceder al servidor también podemos modificar el fichero hosts para usar otra dirección en vez de la dirección IP.  
Para ello modificaremos el archivo hosts con el siguiente comando:  
```
sudo nano /etc/hosts
```  
Nos abrirá un archivo que podremos modificar. Pondremos la dirección IP a la que queremos acceder y separado por un espacio la direccion con la que querremos acceder.  
```
127.0.0.1 sergio.azogue
```  
Por defecto Apache viene con una web ya creada (A la que accedemos por primera vez con la IP). Podemos modificar como maneja las peticiones y tener varias webs en el mismo servidor modificando el fichero de virtual hosts. A continuación vamos a crear nuestra propia configuración de virtual host en gci.  
  
Para empezar crearemos una nueva carpeta para nuestra web con el siguiente comando:  
```
sudo mkdir /var/www/gci
```  
Ahora crearemos el documento de la web dentro de esta ruta. Usaremos el siguiente comando para acceder a la carpeta creada.  
```
cd /var/www/gci
```  
Aqui crearemos el archivo con el siguiente comando:  
```
sudo > index.html
```  
Y lo editaremos con el siguiente:  
```
sudo nano index.html
```  
A continuación vamos a editar el archivo de configuración de Apache. Para ello vamos al directorio donde se encuentra con el siguiuente comando:  
```
cd /etc/apache2/sites-available/
```  
Apache viene con un arhcivo de configuración por defecto el cual usaremos de base para configurar uno nuevo. Para empezar haremos una copia del documento con otro nombre con el siguiente comando:  
```
sudo cp 000-default.conf gci.conf
```  
Y procedemos a editarlo con:  
```
sudo nano gci.conf
```  
Deberiamos de tener nuestro correo en la linea de _ServerAdmin_:  
```
ServerAdmin nuestroCorreo@gmail.com
```  
Además, debemos de editar la linea _DocumentRoot_ para que nuestra web apunte al directorio correcto donde se encuentren nuestras páginas de tal forma:  
```
DocumentRoot /var/www/gci
```  
El archivo de configuración por defecto no viene con la linea _ServerName_ por lo que se la añadiremos:  
```
ServerName gci.ejemplo.com
```  
Tras configurarlo, debemos activar el archivo de configuración ejecutando el siguiente comando en el directorio donde se encuentran los archivos de configuración:  
```
sudo a2ensite gci.conf
```  
Nos devolverá un mensaje indicando que debemos ejecutar un _reload_ para que se active por lo que ejecutaremos lo siguiente:  
```
sudo service apache2 reload
```  
Nuestra web ya deberia de funcionar.
![](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/2X/7/7d6944922296826f70f27ec9b5eff67bd7f46158.png)  
## Bibliografía:  
https://ubuntu.com/tutorials/install-and-configure-apache#3-creating-your-own-website
