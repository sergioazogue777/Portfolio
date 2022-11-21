# Instalación Tomcat en Ubuntu
> Por Sergio Azogue  
  
En este documento repasaremos paso a paso como instalar y configurar tomcat. Para ello deberemos de instalarlo, habilitar puertos y configurar un archivo para crear un usuario con el que acceder al gestor.  

### Instalación  
Para empezar actualizaremos los repositorios con:  
```
sudo apt update
```  
Antes de instalar tomcat es necesario tener java instalado en nuestro equipo. Para instalarlo ejecutaremos el siguiente comando:  
```
sudo apt install openjdk-11-jdk
```  
Despues, verificaremos la versión de java con:  
```
java -version
```  
Una vez instalado, comprobaremos si el paquete de _Apache Tomcat_ esta disponible en el repositorio:  
```
sudo apt-cache search tomcat
```  
Nos devolverá los paquetes disponibles y comprobaremos que está. Una vez comprobado los instalaremos.  
```
sudo apt install tomcat9 tomcat9-admin
```  
Nos pedirá confirmación con lo que aceptaremos tecleando la letra _y_.  
  
Tomcat empieza a funcionar automaticamente tras la instalación. Para comprobar el funcionamiento de los puertos (8080 es el que usa Tomcat) usaremos el siguiente comando:  
```
ss -ltn
```  
En caso de que el firewall este activo puede dar problemas de conectividad, por lo que ejecutaremos la siguiente linea para permitir conexión al puerto 8080 desde cualquier origen:  
```
sudo ufw allow from any to any port 8080 proto tcp
```  
Para comprobar el funcionamiento escribiremos nuestra ip separado de _:_ y el puerto al que queramos acceder en este caso 8080, con lo que pondremos en el navegador:  
```
127.0.0.1:8080
```  
Nos debería aparecer la siguiente ventana:  
![](https://linuxhint.com/wp-content/uploads/2020/06/word-image-22-768x440.png)  
  
 
Antes de usar la aplicación de Tomcat debemos crear un nuevo usuario.  

Para empezar debemos de editar el archivo que contiene los usuarios con el siguiente comando:  
```
sudo nano /etc/tomcat9/tomcat-users.xml
```  
Y escribiremos las siguientes lineas:  
```
<role rolename="admin-gui"/>

<role rolename="manager-gui"/>;

<user username="tomcat" password="nuestraContraseña" roles="admin-gui,manager-gui"/>
```  
Guardaremos el archivo y reiniciaremos tomcat con el siguiente comando:  
```
sudo systemctl restart tomcat9
```  
Una vez configurado deberemos de acceder con el navegador al siguiente enlace para poder acceder al gestor de tomcat:  
```
http://127.0.0.1:8080/manager/html
```  
Introduciremos el usuario y contraseña que hemos puesto en el xml y ya estariamos en el gestor con tomcat funcionando. Ls ventana que debería aparecer es la siguiente:    
![](https://linuxhint.com/wp-content/uploads/2020/06/word-image-33-768x493.png) 
