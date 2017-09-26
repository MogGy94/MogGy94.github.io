---
layout: post
title: "Algoritmos De Rastering "
date: 2017-09-26
categories:
  - algoritmos
description: Descripcion sobre algunos algortimos de rastering
image: http://ddragon.leagueoflegends.com/cdn/img/champion/splash/Azir_0.jpg
image-sm: https://unsplash.it/500/300?image=1003
---

# Algoritmos de rastering   

## El problema de la EPO   
La Eliminaci´on de Partes Ocultas (EPO), consiste en calcular las regiones o pixels de la imagen que ocupa
cada objeto del modelo.   

* Decir que un punto x de las superficies de los objetos es visible quiere decir que:    
V(x, o) = 1   
donde o es la posici´on del observador   
* Lo anterior es equivalente a x = P(o, wox) (donde wox es el vector unitario desde o hacia x)   
* Se trata de encontrar los puntos o regiones visibles de la escena, de forma que se puedan mostrar en
un dispositivo.   

## Tipos de algoritmos  
Basicamente hay dos tipos de algoritmos para Eliminaci ´ ´on de Partes Ocultas (EPO)   

* Algoritmos con precision de imagen
se trata de determinar que objeto es visible en el centro de cada pixel
* Algoritmos con precision de objetos 
se trata de determinar que parte de los caras o que parte de las arista de un modelo son
visibles   


# Z-buffer 

## El algoritmo Z-buffer   

• Ideado por E.Catmull en 1974, necesita un array bidimensional (Z-buffer), con una entrada por cada
pixel   

• En dicho array se guarda la profundidad en Z del objeto que se proyecta en cada pixel.   
• Es el mas facil de implementar en hardware   
• Los pol´ıgonos se dibujan secuencialmente, no hay necesidad de almacenarlos en una lista (solo se
ocupa memoria con el Z-buffer)  

## El frame-buffer (o color buffer) y el Z-buffer   

Estos dos buffers tienen la misma resoluci´on, para cada pixel:  

• el frame-buffer contiene una terna RGB (= color del pol´ıgono)   
• el z-buffer contiene un valor real (= distancia observador-pol´ıgono)   
Z-buffer (distancias) Imagen (colores)     

## Caracter´ısticas del algoritmo Z-buffer  

• El Z-buffer se inicializa con un valor menos infinito    
• Cada pol´ıgono se dibuja por l´ıneas de barrido (ver relleno de pol´ıgonos en IG)   
• Antes de dibujar cada pixel, se calcula la profundidad en Z del pol´ıgono en el pixel   
• Si el pol´ıgono es visible en el pixel se actualizan el Z-Buffer y la imagen   
• En caso contrario, no se hace nada   


## Incremento de Z entre pixels adyacentes   

• El calculo de la ´ Z en cada pixel puede hacerse incrementalmente   
• La diferencia en Z entre pixels adyacentes es constante en un pol´ıgono   
• Esta diferencia se nota con ∆z y es f(x + 1, y) − f(x, y), luego:   
f(x, y) = ex + gy + h   
∆z = f(x + 1, y) − f(x, y)    
= e(x + 1) + gy + h − ex − gy − h    
= e = − a/c   
= −nx/nz   
• ∆z solo depende de la normal del polıgono   

### Esquema del algoritmo Z-Buffer

#### Procedimiento ZBuffer( lista pol´ıgonos L )

##### * Inicializar Z Buffer e imagen    
Paracada p ol´ı g o n o P en L   
Sea ∆z := − nx/nz   
Paracada l´ı n e a de b a r r i d o ocupada po r P   
( l´ı n e a a a l t u r a y , e n t r e x0 y x1 )    
x := menor e n t e r o mayor o i g u a l que x0   
z := f(x, y)(=p r o f u n di d a d en Z de P en (x, y) )   
Mient ras que x < x1   
Si z > ZBuffer[x, y] e nt o nc es   
Imagen[x, y] := c o l o r de P   
Z b u f f e r[x, y] := z   
z := z + ∆z   
x := x +   

## Referencia 
Visualizaci´on y Realismo:   
Capıtulo 2. Eliminaci´on de Partes Ocultas   
Carlos Urena Almagro ˜   
Curso 2011-12   