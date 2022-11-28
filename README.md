# Proyecto_SRI1
Repositorio donde se almacena el proyecto de primer trimestre del modulo SRI
## Servidor con wordpress
Lo primero antes de empezar es instalar php, mysql, apache2, es decir tener LAMP, suponemos que ya tenemos la maquina linux sin apache ni php ni mysql, lo primero que tenemos que hacer es instalar apache como super usuario, para esto:
```bash
$ sudo su
$ apt install apache2
```
Para comprobar que se ha instalado debemos hacer systemctl status apache2
```bash
$ systemctl status apache2
```
![image](https://user-images.githubusercontent.com/91255763/204372625-2ecbcc3b-ca82-4ea9-9aa0-a7203bfa854c.png)

Ahora que tenemos apache debemos crear el directorio para centro.intranet, para ello debemos movernos a la carpeta www de apache2:
```bash
$ mkdir /var/www/centro.intranet
$ ls /var/www
```
![image](https://user-images.githubusercontent.com/91255763/204373513-b70406a3-ac3f-4616-937d-c34d5d146eac.png)
Ahora debemos instalar Mysql, para ello:
```bash
$ apt update
$ apt install mysql-server
```
Para comprobar si esta instalado 
```bash
systemctl 
Después debemos configurar Mysql
```bash
mysql_secure_installation
```

