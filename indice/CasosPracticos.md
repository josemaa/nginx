# Nginx

 
## Casos practicos

*Vamos a mostrar acontinuación los casos practicos por apartados y estaran enlazados a una pagina aparte donde estara los codigos de cada apartado*

### 1.-Version Nginx Instalada
 
 ```nginx -v```


<img src=/capturas/apartadoA.png width=600px>


### 2.-Servicio Asociado
 
 ```systemctl status nginx```


<img src=/capturas/serAsociado.png width=600px>


### 3.-Ficheros de configuracion
 
 Los ficheros de configuracion los podemos encontrar en ```/etc/nginx```, y el fichero el cual contiene la configuración basica y general es ```nginx.conf```


<img src=/capturas/ficheroconf.png width=600px>

### 4.-Pagina web por defecto
 
 * Siempre es aconsejable hacer copia del index inicial por si lo necesitamos:
 
```cp /var/www/html/index.nginx-debian.html /var/www/html/index.nginx-debian.html.ORIGINAL```


* Cambiamos el nombre a index.html del archivo para que sea mas facil

```mv /var/www/html/index.nginx-debian.html /var/www/html/index.html```

* Modificamos el index con el siguiente comando

``` echo "<h1> Bienvenidos a Mi servidor web de nginx, espero que les guste </h1> > /var/www/html/index.html```

<img src=/capturas/paginadefecto.png width=600px>

### 5.-Virutal Hosting

 **Tenemos dos sitios virtuales con la misma ip y con el mismo puerto, entonces vamos a configurarlos cada sitio virtual con un dominio distinto, web1 tendra el dominio (www.web1.org) y web2 tendra el dominio (www.web2.org).**

* Creamos dos carpetas a la misma altura de /var/www/html (contendran las paginas de cada web)

```mkdir /var/www/html/web1 /var/www/html/web2```

  - Introducimos un index.html basico que las identifique
  
  ```echo "<h1> Bienvenida a la pagina web1 </h1>" > /var/www/web1/index.html```
  
  ```echo "<h1> Bienvenida a la pagina web2 </h1>" > /var/www/web2/index.html```
  
   
   <img src=/capturas/carpetas.png width=600px>
    
   - Copiamos el fichero general que es ```/etc/nginx/sites-avaible/default``` y con el configuramos las paginas nueva y creamos un enlace duro ```/etc/nginx/sites-enabled```
   
  ```cp /etc/nginx/sites-available/default /etc/nginx/sites-available/web1```
  ```cp /etc/nginx/sites-available/default /etc/nginx/sites-available/web2```
    
    `ln -s /etc/nginx/sites-available/web1 /etc/nginx/sites-enabled/` 
    `ln -s /etc/nginx/sites-available/web2 /etc/nginx/sites-enabled/` 
  
  - Configuramos los ficheros de nuestras paginas web de la siguiente manera:
  
 [Fichero web1](https://github.com/josemaa/nginx/blob/main/web1) 
    
 [Fichero web2](https://github.com/josemaa/nginx/blob/main/web2)
 
 
  - Al no tener un servidor dns y poder agregarlos a las zonas directa e inversa, lo debemos añadir manualmente al /etc/hosts
   
    **Maquina servidor**
    
    ```/etc/hosts```
    
     <img src=/capturas/dns1.png width=600px>
     
      **Maquina cliente**
    
    ```/etc/hosts```
    
     <img src=/capturas/dns2.png width=600px>
  
   **Si no funciona reiniciamos servicio**
   
   * Buscamos www.web1.org y www.web2.org
    
### 6.-Control de Acceso: A la web1 se podrá acceder tanto desde la red externa como interna, a la web2, solo de la interna.

 * Editamos el fichero de configuracion de la web2 añadiendo las siguientes lineas:
   Fichero ----> ```/etc/nginx/sites-avaible/web2```
   
   ```location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		try_files $uri $uri/ =404;
		allow 192.168.3.0/24;
		deny all;
	}```
 
  <img src=/capturas/ControlAcceso.png width=600px>
  
  * Reiniciamos el servicio
  * Comprobamos
     - Red Externa

 <img src=/capturas/Redexterna.png width=600px>
 
   -  Red Interna

 <img src=/capturas/Redinterna.PNG width=600px>
 
 
 ### 7.-Autentificacion Usuario
 
 **Creamos un directorio web1 que se llame privado y al cual solo pueden acceder usuarios validos**

 * Crearemos el directorio ```/var/www/web1/privado```
 
 ```mkdir privado```

<img src=/capturas/autentificacion.png width=600px>


* Añadimos las siguientes lineas en el fichero de configuracion de web1 ```/etc/nginx/sites-avaible/web1```
 
 
<img src=/capturas/autentificacion2.png width=600px>

* Instalamos el paquete apache2-utils

 ```apt install apache2-utils```
 
 * Creamos las credenciales en el fichero del usuario

 ```cd /etc/nginx```
 ```htpasswd -c -m .htpasswd usuario```
 
 **Nuestro usuario seria, usuario y el archivo que contiene todo es .htpasswd.
 -c ---> crea un fichero
 -m ---> obliga la encriptacion MD5**
 
  <img src=/capturas/autentificacion3.png width=600px>
 
 - Reiniciamos servicio
  ```systemctl restart nginx.service```
 
 * Comprobamos
 
 <img src=/capturas/autentificacion4.png width=600px>
 
### 8.-Red interna no pide autentificacion y externa si

* Añadimos las siguientes lineas al codigo y comprobamos:

<img src=/capturas/autentificacion5.png width=600px>

* Reiniciamos

```systemctl restart nginx.service```
 
 
 
 
 

 

  

