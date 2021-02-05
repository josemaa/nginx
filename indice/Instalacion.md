# Nginx 

 
## Instalacion

*Antes que nada nos metemos en nuestros servidor con ssh*


<img src=/capturas/instalacion1.png width=600px>

 >> Esto nos saldria al no tener instalado el nginx

<img src=/capturas/instalacion3.png width=600px>

*Una vez nos hemos metido remotamante con ssh, lo que debemos hacer es compobar el paquete si esta instalado, si no lo esta procedemos a instalarlo pero antes debemos hacer un update*

- Comprobamos el paquete
```apt policy nginx```
- Instalamos el paquete
```apt install nginx```
- Activamos el demonio para que se inicie nginx cuando arranquemos el servidor
```systemctl enable nginx```
- Reiniciamos Servicio
```systemctl restart nginx```



<img src=/capturas/instalacion2.png width=600px>

*Una vez hagamos hecho los pasos anteriores procedemos a verificar que funciona correctamente*

<img src=/capturas/instalacion4.png width=600px>



