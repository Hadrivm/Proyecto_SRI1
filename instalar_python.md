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
![image](https://user-images.githubusercontent.com/91255763/204559096-d9429bf5-78c8-4971-928c-162d4ca3ddfb.png)


Para comprobar que funciona nos movemos al navegador y escribimos 
```bash
http://ip_del_server
```
![image](https://user-images.githubusercontent.com/91255763/204578733-e59e1e66-24c6-4623-a86c-8a60650e9a3d.png)

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
si queremos comprobar que el sitio existe vamos al navegador y escribimos www.departamentos.centro.intranet 

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
