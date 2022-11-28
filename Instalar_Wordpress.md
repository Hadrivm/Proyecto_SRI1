### Instalación de Apache
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
![image](https://user-images.githubusercontent.com/91255763/204378081-a3392769-9dce-4b38-a520-906a0ef829f7.png)


Para comrpobar que funciona nos movemos al navegador y escribimos 
```bash
http://ip_del_server
```
![image](https://user-images.githubusercontent.com/91255763/204378218-54848d7a-9c7f-4683-a55f-3895f5c0d849.png)

Ahora que tenemos apache debemos crear el directorio para centro.intranet, para ello debemos movernos a la carpeta www de apache2:
```bash
$ mkdir /var/www/centro.intranet
$ ls /var/www
```
![image](https://user-images.githubusercontent.com/91255763/204373513-b70406a3-ac3f-4616-937d-c34d5d146eac.png)

Y le  asignamos una ip a centro.intranet de la misma manera que la revisamos antes:

```bash
$ cd /etc
$ nano hosts
```
y cuando lo terminemos de editar ctrl+o y ctrl+x
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
Para instalar php se introducen los siguiente coamndo
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
