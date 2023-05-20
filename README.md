# Instalación de NGINX en Ubuntu Mate

1. Abre una terminal en Ubuntu Mate.

2. Actualiza los paquetes del sistema ejecutando el siguiente comando:
```
sudo apt update
```
3. Luego, instala Nginx ejecutando el siguiente comando:
```
sudo apt install nginx
```
4. Durante la instalación, se te pedirá que ingreses tu contraseña de administrador.

5. Una vez completada la instalación, Nginx se iniciará automáticamente. Puedes verificar si Nginx está funcionando correctamente abriendo un navegador web e ingresando la dirección IP de tu servidor en la barra de direcciones. Deberías ver la página de bienvenida de Nginx.

6. Abre el archivo de configuración predeterminado de Nginx utilizando un editor de texto. En Ubuntu Mate, puedes hacerlo ejecutando el siguiente comando:
```
sudo nano /etc/nginx/sites-available/default
```
7. Dentro del archivo de configuración, encuentra la sección server y comenta (agregando un símbolo # al principio de la línea) o elimina cualquier configuración existente dentro de ella.

8. Agrega la siguiente configuración para configurar el proxy inverso:
```
server{
  listen 80 default server;
  listen [::]:80 default_server;

  location /apache{
    proxy_pass http://172.20.10.8/;
    proxy_set_header host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
  location /compose{
    proxy_pass http://172.20.10.9/;
    proxy_set_header host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}  
```
9. Configuramos las interfaces de red en sistema, el siguiente comando proporciona información detallada sobre las interfaces de red, como direcciones IP, máscaras de red, direcciones MAC, estadísticas de tráfico y más:
```
/home/composel# ifconfig
```
10. Ahora, utilizamos este comando para verificar la conectividad entre tu máquina y una dirección IP de NGINX.
```
/home/composel# ping 172.20.19.7
```
11. Utilizamos este comando para listar los contenedores en ejecución en Docker. 
```
/home/compose1# docker ps
```
12. Ahora, utilizamos este comando para iniciar el servidor web Nginx utilizando la configuración predeterminada.
```
/home/compose1# nginx
```
13. Debemos localizar y modificar el archivo de Docker:
```
/home/compose1# cd ~
~# cd myapp
~/myapp# docker-compose down
~/myapp# docker-compose up -d
~/myapp# docker ps
~/myapp# docker exec -it myapp_web_l sh
```
14. Actualizamos la lista de paquetes disponibles.
```
/home/maestro21# apt-get update
```
15. Usamos este comando para instalar pip
```
/home/maestro21# apt-get install python3-pip
```
16. Ahora, instalamos ray a partir de pip
```
/home/maestro21# pip install ray
``` 

Llegado a este punto, ray se instala sin ningún problema, pero al ejecutar el siguiente comando:
```
Ray -version
```
la terminal nos indica que ray no se encuentra instalado.
