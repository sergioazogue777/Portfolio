# Examen  
Por **Sergio Azogue**  
En este documento se redactará la resolución de los ejercicios del examen del primer timestre. Se realizarán en un equipo todos los ejercicios, a excepción del SSH el cual requerirá un ordenador externo al que conectarse.  
Describiremos los pasos a seguir para conectarse a un equipo externo y decargar una imagen en una carpeta que hayamos creado. Además, en nuestro propio equipo, deberemos modificar un fichero para que, accediendo mediante una ip dada, muestre una web que contengamos en nuestro equipo.  
  
## Índice
* Ejercicios
  1. Ejercicio 2: SSH  
  1. Ejercicio 3: Command line  
  1. Ejercicio 4: VirtualHost  
* Bibliografía  
* Conclusiones  
## Ejercicios  
### Ejercicio 2
Para acceder mediante ssh a un equipo primero debemos comprobar que tenemos ssh. Para instalarlo ejecutaremos el siguiente comando:  
```
sudo apt install ssh
```  
Una vez instalado procederemos a conectarnos usando la siguiente sintaxis:  
```
ssh nombreUsuario@nombreServidor
```  
El comando que he puesto en cuestión:  
```
ssh usuario@192.168.0.168
```  
Nos pedirá una contraseña la cual introduciremos.  
  
Para comprobar que hemos cambiado de usuario podemos ejecutar el siguiente comando que devolverá nuestro nombre de usuario:  
```
whoami
```  
Lo siguiente que nos pide es acceder a la carpeta _/var/www_ y crear una carpeta llamada como nuestro nombre. Para acceder a dicha carpeta usaremos el siguiente comando:  
```
cd /var/www
```  
Una vez dentro del directorio crearemos la carpeta con nuestro nombre usando el siguiente comando:  
```
mkdir nuestroNombre
```  
En mi caso he puesto el siguiente comando:  
```
sudo mkdir sergioAzogue
```  
Para finalizar el ejercicio crearemos un archivo _.txt_ dentro de la carpeta recien creada. Para ello accederemos a la carpeta con el siguiente comando:  
```
cd sergioAzogue
```  
Antes de poder crear el archivo necesitaremos super usuarios con lo que ejecutaremos el siguiente comando:  
```
sudo su
```  
Y una vez dentro y siendo super usuarios crearemos el archivo _ejercicio2.txt_ con el siguiente comando:  
```
> ejercicio2.txt
```  
  
### Ejercicio 3  
  
El Siguiente ejercicio pide descargar una imagen dentro de la carpeta que hemos creado por linea de comandos.  
Para evitar algún fallo de permisos me he puesto como super usuario con el comando:  
```
sudo su
```  
Asumiendo que estamos dentro de la carpeta que hemos creado ejecutaremos el siguiente comando:  
```
wget enlaceALaImagen
```  
En mi caso he ejecutado el siguiente comando:  
```
wget https://iesalandalus.org/ciclos/semipresencial/daw-sp/daw.png
```  
Y ya tendriamos la imagen descargada dentro del directorio.  
### Ejercicio 4  
Para realizar este ejercicio debemos de usar nuestro equipo local asi que tendremos que salir del ssh con el comando:  
```
exit
```  
Una vez en nuestro equipo para poder añadir un virtual host deberemos modificar el archivo /etc/hosts. Para ello con ejecutar el siguiente comando será suficiente:  
```
sudo nano /etc/hosts
```  
Una vez dentro del archico escribiremos nuestra propia IP en una linea y separado por una tabulación el nombre con el que queremos acceder en mi caso _daw.ejercicio4.com_, de esta forma:  
```
127.0.0.1       daw.ejercicio4.com
```  
En ese caso he usado la dirección loopback para que acceda a mi propio equipo pero también podría haber usado la dirección que aparece con el siguiente comando:  
```
hostname -I
```  
Con el que la dirección que usaremos es diferente:  
```
192.168.0.138       daw.ejercicio4.com
```  
Para que nos aparezca el archivo con nuestro nombre deberemos de crear ese mismo archivo dentro de la carpeta donde se encuentre el serverRoot en el archivo de configuración de Apache. Además de añadir el siguiente módulo con el que al acceder a la IP se abrirá automaticamente:  
```
DirectoryIndex nombreDelArchivo.html
```  
Para comprobar que funciona deberemos de introducir el nombre que le hemos dado en la barra de búsqueda de un navegador. Imprimirá el documento que le hemos indicado en _DirectoryIndex_.  

## Bibliografía  
Tutorial de Apache:  [enlace](https://stackoverflow.com/questions/19322345/how-do-i-change-the-default-index-page-in-apache)
  
## Conclusiones 
SSH nos ha ayudado a acceder a los directorios de un equipo remoto, además de operar con el con funciones como descargas de internet, crear directorios y ficheros.  
  
A su vez también se ha demostrado la funcionalidad del archivo _hosts_ y lo sencillo que podemos hacer el acceso a un servidor sin necesidad de estar poniendo su dirección IP.
