# Comparativa con Apache
  
## Que ventajas presenta nginx frente apache

  La principal diferencia entre Apache y Nginx (y la más grande) es su arquitectura, mientras que Apache abre un montón de procesos para servir peticiones, Nginx abre solo los hilos de ejecución justos y necesarios permitiendo servir millones de peticiones en un corto espacio de tiempo, ya que no requiere tiempo adicional para abrir nuevos procesos y además al no abrir nuevos procesos tampoco consume mas memoria RAM.

## Introduccion

 La principal diferencia entre Apache y Nginx (y la más grande) es su arquitectura, mientras que Apache abre un montón de procesos para servir peticiones, Nginx abre solo los hilos de ejecución justos y necesarios permitiendo servir millones de peticiones en un corto espacio de tiempo, ya que no requiere tiempo adicional para abrir nuevos procesos y además al no abrir nuevos procesos tampoco consume mas memoria RAM.

La diferencia de rendimiento entre Nginx y Apache se nota, ya que el tiempo de respuesta conseguido por Nginx es casi un 150% más rápido que en el caso de Apache.

* En el siguiente grafico puedes ver un gráfico de comparación de tiempo de respuesta entre Nginx y Apache:

 
 ![captura1.png](/capturas/captura1.png)

* Y en el siguiente gráfico puedes ver un gráfico donde puedes apreciar el consumo de memoria RAM en el servidor de Apache y de Nginx:

 ![captura2.png](/capturas/captura2.png)


 
