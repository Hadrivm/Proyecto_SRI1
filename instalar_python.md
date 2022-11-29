### Instalar Apache
Para instalar apache debemos primero estar en modo sudo su:
```bash
$ sudo su
$ apt update
$ apt install apache2
```
Para comprobar que se ha instalado debemos hacer systemctl status apache2
```bash
$ systemctl status apache2
```
![image](https://user-images.githubusercontent.com/91255763/204372625-2ecbcc3b-ca82-4ea9-9aa0-a7203bfa854c.png)

Ahora debemos ajustar el cortafuegos para permitir el tráfico web:
```bash
$ ufw app list
```
![image](https://user-images.githubusercontent.com/91255763/204376644-33900e2d-61c5-46da-9b10-930c1df3d1bc.png)

```bash
$ ufw app info "Apache Full"
```
![image](https://user-images.githubusercontent.com/91255763/204377064-3b60570f-cbb7-4a45-a2ad-ee7873e5ee75.png)

Para saber la ip del localhost hacemos:

```bash
$ cd/etc 
$ nano hosts
y cuando lo terminemos de editar ctrl+o y ctrl+x
```
![image](https://user-images.githubusercontent.com/91255763/204579317-a1a53500-7292-4a21-814d-3ade1d83ed1c.png)



Para comprobar que funciona nos movemos al navegador y escribimos 
```bash
http://ip_de_localhost
```

![image](https://user-images.githubusercontent.com/91255763/204579694-8518ac55-a687-4f3b-bfb1-f393213e7eb3.png)


Ahora que tenemos apache debemos crear el directorio para departamentos.centro.intranet, para ello debemos movernos a la carpeta /www de apache2:

```bash
$ mkdir /var/www/html/departamanetos.centro.intranet
$ ls /var/www/html
```
![image](https://user-images.githubusercontent.com/91255763/204560290-73b5f451-7bfd-420c-b252-9da2b70e5e7b.png)

Y le  asignamos una ip a departamentos.centro.intranet y a www.departamentos.centro.intranet  de la misma manera que la revisamos antes:

```bash
$ cd /etc
$ nano hosts
```
y cuando lo terminemos de editar ctrl+o y ctrl+x

![image](https://user-images.githubusercontent.com/91255763/204578502-b1d47218-fe71-46ce-8502-6c4980389d93.png)


Para que el sitio sea visible debermos crear un virtual host en el fichero sites-available de /etc/apache2
```bash 
$ nano /etc/apache2/sites-available/departamentos.centro.intranet.conf
```
```apache2
<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    ServerAlias www.departamentos.centro.intranet
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/departamentos.centro.intranet
    Errorlog ${APACHE_LOG_DIR}error.log
    Customlog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Después debemos dar de alta el sitio con 

```bash
$ a2ensite departamentos.centro.intranet
```
si queremos comprobar que el sitio existe vamos al navegador y escribimos http://www.departamentos.centro.intranet o http://departamentos.centro.intranet 

![image](https://user-images.githubusercontent.com/91255763/204577842-399c5b04-251f-4978-adc4-98726523704b.png)


### Instalación de Mysql
Ahora debemos instalar Mysql, para ello:
```bash
$ apt update
$ apt install mysql-server
```
Para comprobar si esta instalado 
```bash
systemctl status mysql
```
![image](https://user-images.githubusercontent.com/91255763/204375487-df023bc2-9712-4107-b90d-8b8d49bff650.png)

## Instalar PHP
Para instalar php se introducen los siguiente comando

```bash
$ apt install php libapache2-mod-php php-mysql
``` 
En la mayoría de los casos, desearás modificar la forma mediante la cual Apache sirve archivos cuando un directorio es solicitado. En este momento, si un usuario solicita un directorio del servidor, Apache buscará, en primera instancia, un archivo llamado index.html. Nosotros queremos que el servidor web le dé prelación a los archivos PHP sobre cualquier otro archivo. Para lo cual haremos que el Apache busque el archivo index.php en primer lugar.

```bash
$ nano /etc/apache/mods-enabled/dir.conf
```
Su aspecto inicial es el siguiente

![image](https://user-images.githubusercontent.com/91255763/204391170-790abf86-a1fc-4318-b84d-3d1b221c762d.png)

Pero debemos modificarlo para que tenga el siguiente

![image](https://user-images.githubusercontent.com/91255763/204391339-6a2b0756-77a2-4567-98bb-d7705f6f7ce8.png)

Y debemos reiniciar apache

```bash
$ systemctl restart apache2
```
y debemos comprobar el estado de apache2 con:

```bash
$ systemctl status apache2
```
![image](https://user-images.githubusercontent.com/91255763/204391812-fddd3e6a-3b92-4926-a9cb-6b2837abcf05.png)

Con esto ya esta instalado php.

## Preparaciones
Para poder usar una aplicación pythin en el servidor primero debemos instalar un modificador para apache
```bash
$ apt-get install libapache2-mod-wsgi
```

Ahora en el directorio de departamentos.centri.intranet debemis crear otros 2,  mypythonapp y public_html, una almacenara la aplicación python y la otra servira a la aplicación

```bash
$ mkdir /var/www/html/departementos.centro.intranet/mypythonapp
$ mkdir /var/www/html/departementos.centro.intranet/public_html
``` 
![image](https://user-images.githubusercontent.com/91255763/204596640-31f26c18-da5a-4360-9016-c4923f2bd66c.png)

Desde mypythonapp almacenaremos todoa los modulos y paquetes de nueestra aplicación en python mientras que public_html almacenara los archivos estaticos y sera el unico directorio al que se pueda acceder mediante el navegador web. 

Aprovecharemos este paso, para crear una carpeta, destinada a almacenar los logs de errores y accesos a nuestra Web App:

```bash
$ mkdir /var/www/html/departementos.centro.intranet/logs
```
Debemos crear un controlador para la aplicación ya que todas las peticiones realizadas por el usuario (es decir, las URL a las cuáles el usuario acceda por el navegador), serán manejadas por un único archivo, que estará almacenado en nuestro directorio mypythonapp.

Ahora deberomos modificar el virtual host que creamos antes para que quede de la siguinete manera:

```bash
<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    ServerAlias www.departamentos.centro.intranet
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/departamentos.centro.intranet
    WSGIScriptAlias /var/www/html/departamentos.centro.intranet/controller.py 
    Errorlog ${APACHE_LOG_DIR}error.log
    Customlog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Hemos añadido 
```bash
 WSGIScriptAlias /var/www/html/departamentos.centro.intranet/controller.py
 ```
 
```bash
$ echo '# -*- coding: utf-8 -*-' > mypythonapp/controller.py
``` 


