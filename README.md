# Proyecto_SRI1
Repositorio donde se almacena el proyecto de primer trimestre del modulo SRI
## Servidor con wordpress
Lo primero antes de empezar es instalar php, mysql, apache2, es decir tener LAMP, suponemos que ya tenemos la maquina linux sin apache ni php ni mysql.
### Instalación de Apache
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

http://ip_del_server

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





