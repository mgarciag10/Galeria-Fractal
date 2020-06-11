# Geometría Fractal 

## Introducción

## ¿Qué es un fractal?
Un fractal es un objeto cuya estructura se repite a diferentes escalas. Es decir, por mucho que nos acerquemos o alejemos del objeto, observaremos siempre la misma estructura. De hecho, somos incapaces de afirmar a qué distancia nos encontramos del objeto, ya que siempre lo veremos de la misma forma.

## Propiedades de los fractales 
Analizando esta construcción, podemos resumir las principales propiedades que exhiben la mayoría de los fractales
- **Estructura fina:** Al ampliar la curva, por mucho que la amplifiquemos, las irregularidades en su forma siempre son evidentes. Esta es una consecuencia directa de la construcción en la que los segmentos de línea muy pequeños se trataron de la misma manera que el original pero en una escala mucho menor.
- **Auto-similitud:** La curva está compuesta de pequeñas copias de sí misma.
- **Los métodos clásicos de geometría y matemáticas no son aplicables:** La figura es demasiado irregular para ser descrito en el lenguaje geométrico tradicional y, a diferencia de las formas clásicas, no puede expresarse mediante una fórmula "simple".
- **El tamaño depende de la escala a la que se mide:** A diferencia de figuras tradicionales como el círculo, dónde podemos tratar de medir la longitud tomando pequeños tramos y multiplicando por el número de pasos; tratar de medir la longitud de la curva de Koch dividiéndola en pasos cada vez más cortos solo proporciona estimaciones cada vez mayores para su longitud.
- **Una construcción recursiva simple:** Si bien la curva parece un objeto complejo, en realidad se trata de una construcción recursiva que consiste en aplicar unos pasos simples una y otra vez.
- **Una apariencia natural:** Con un poco de imaginación, la mayoría de los objetos fractales toman formas que recuerdan a la Naturaleza.

## Clasificación de los fractales 
Esta se establece a partir del origen de su formación:
- **Lineales:** Se generan a partir de conceptos y algoritmos lineales, como por ejemplo rectas o triángulos. Pueden obtenerse mediante trazados geométricos simples.
- **Complejos:** Se generan mediante un algoritmo de escape. Para cada punto se calculan una serie de valores mediante la repetición de una formula hasta que se cumple una condición, momento en el cual se asigna al punto un color relacionado con el número de repeticiones. 
Los fractales de este tipo precisan de millones de operaciones, por lo cual sólo pueden dibujarse con la ayuda del ordenador.
- **Órbitas caóticas:** Este tipo de modelo nació con un estudio sobre órbitas caóticas desarrollado por Edward  Lorenz en 1.963. El atractor de Lorenz tiene un comportamiento fractal, aunque los fractales no son sinónimos y tienen comportamientos distintos; solamente comparten una formulación sencilla.
- **Autómatas celulares:** Los autómatas celulares fueron utilizados por primera vez por los matemáticos John von Neumann y Stanislaw Ulam en 1948 para representar la reproducción en algunos sistemas biológicos.
Un autómata celular es un sistema dinámico discreto, (espacio y tiempo toman valores discretos), cuya función asociada toma un conjunto finito de valores. Funcionan con sencillas reglas que colorean zonas a partir del color de las adyacentes.
- **Plasma:** Estructuras como el plasma o las imágenes de difusión dependen en cierta medida del azar, por lo cual son únicas e irrepetibles.
Ello se debe a que no es un proceso determinista, sino totalmente aleatorio. Consiste en un patrón único e irrepetible de colores.

## Tipos de Fractales 
Algunos ejemplos de fractales son:

### Conjuntos de Newton
El fractal de Newton es una curiosa creación basado en la aplicación del método de Newton para la resolución de sistemas de ecuaciones no lineales. El algoritmo es eficiente para encontrar aproximaciones de los ceros o raíces de una función real. También puede ser usado para encontrar el máximo o mínimo de una función, encontrando los ceros de su primera derivada.

La idea de este método es la siguiente: se comienza con un valor razonablemente cercano al cero (denominado punto de arranque), entonces se reemplaza la función que estamos tratando por la recta tangente en ese valor, se iguala a cero y se despeja. Este cero será, generalmente, una aproximación mejor a la raíz de la función. Luego, se aplican tantas iteraciones como se deseen hasta que el método de una solución adecuada. Cabe destacar que es posible que el método diverja en determinadas circunstancias que pueden depender de la elección del punto inicial.

Además es responsabilidad nuestra la elección de un buen test de parada, aunque dicho test podría basarse simplemente en el número de iteraciones realizadas.

<img src="https://latex.codecogs.com/svg.latex?\Large&space;x_{n+1}=x_{n}-\frac{f(x_{n})}{f'(x_{n})}" />

Partiendo de este método, y dado que es capaz de aproximarse tanto a soluciones reales como a complejas, podríamos ingeniárnoslas para que dada una función se coloreasen de forma distinta las soluciones a las que el algoritmo va convergiendo. En pocas palabras: seleccionamos una región del plano complejo y vamos ejecutando el método de Newton, para una función <img src="https://latex.codecogs.com/svg.latex?\Large&space;f" /> dada, en un punto elegido de la región. Dependiendo de a qué solución converge el método pintamos ese punto de un color u otro.

Como podemos comprobar, en este caso, han surgido fractales a partir de un método de aproximación de raíces de funciones y un poco de imaginación.

Para los ejemplos que se verán en las simulaciones se han dibujado los fractales basados en las siguientes funciones:

#### Primer Fractal
![Primer Fractal - Conjunto de Newton](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/newton%201.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=z^{3}-(z-1)^{2}-1" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-1
xb=1
ya=-1
yb=1
maxit=202
h=1e-6
eps=1e-3

def f(z):
    return z**3-(z-1)**2-1

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            dz=(f(z+complex(h,h))-f(z))/complex(h,h)
            z0=z-f(z)/dz
            if abs (z0-z)<eps:
                break
            z=z0
            r=i*50
            g=i*20
            b=i*30
            image.putpixel((x,y),(r,g,b))
image
```

#### Segundo Fractal
![Segundo Fractal - Conjunto de Newton](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/newton%202.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=z^{5}+z^{4}-z^{3}+z^{2}-z+10" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-1
xb=1
ya=-1
yb=1
maxit=202
h=1e-6
eps=1e-3

def f(z):
    return z**5+z**4-z**3+z**2-z+10

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            dz=(f(z+complex(h,h))-f(z))/complex(h,h)
            z0=z-f(z)/dz
            if abs (z0-z)<eps:
                break
            z=z0
            r=i*10
            g=i*11
            b=i*20
            image.putpixel((x,y),(r,g,b))
image
```

#### Tercer Fractal
![Tercer Fractal - Conjunto de Newton](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/newton%203.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=(z^{2}-4)(z^{3}-10)+2" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-1
xb=1
ya=-1
yb=1
maxit=202
h=1e-6
eps=1e-3

def f(z):
    return (z**2-4)*(z**3-10)+2

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            dz=(f(z+complex(h,h))-f(z))/complex(h,h)
            z0=z-f(z)/dz
            if abs (z0-z)<eps:
                break
            z=z0
            r=i*10
            g=i*20
            b=i*11
            image.putpixel((x,y),(r,g,b))
image
```

#### Cuarto Fractal
![Cuarto Fractal - Conjunto de Newton](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/newton.png)
##### Función 
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=-z^{5}+z^{3}-z+4" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-1
xb=1
ya=-1
yb=1
maxit=202
h=1e-6
eps=1e-3

def f(z):
    return -z**5+z**3-z+4

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            dz=(f(z+complex(h,h))-f(z))/complex(h,h)
            z0=z-f(z)/dz
            if abs (z0-z)<eps:
                break
            z=z0
            r=i*21
            g=i*20
            b=i*10
            image.putpixel((x,y),(r,g,b))
image
```


### Conjuntos de Julia
Podemos definir el conjunto de Julia de un polinomio de variable compleja como la frontera del conjunto de puntos que escapan al infinito al iterar dicho polinomio. Esto significa que la órbita de un elemento del conjunto de Julia no escapa al infinito, pero existen puntos arbitrariamente cerca de él que sí lo hacen. 

Julia probó que la órbita de z = 0 juega un papel esencial para saber si un conjunto de Julia es conexo. ¿Cuándo podemos considerar que la órbita de z = 0 diverge a infinito? La teoría de iteraciones nos asegura que la órbita divergirá a infinito si en algún momento uno de sus puntos tiene módulo mayor o igual a 2.

A continuación veremos algunos ejemplos: 

#### Primer Fractal
![Primer Fractal - Conjunto de Julia](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/julia%201.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=z^{4}+c" />
<img src="https://latex.codecogs.com/svg.latex?\Large&space;c=(-0,5-0,5i)" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-2
xb=2
ya=-2
yb=2
maxit=30

def f(z):
    return z**4-complex(0.5,0.5)

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            z0=f(z)
            if abs(z)>1000:
                break
            z=z0
            r=i*15
            g=i*20
            b=i*18
            image.putpixel((x,y),(r,g,b))
image
```

#### Segundo Fractal
![Segundo Fractal - Conjunto de Julia](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/julia%202.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=z^{5}-1+c" />
<img src="https://latex.codecogs.com/svg.latex?\Large&space;c=(0,7+0,7i)" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-2
xb=2
ya=-2
yb=2
maxit=30

def f(z):
    return z**5-1+complex(0.7,0.7)

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            z0=f(z)
            if abs(z)>1000:
                break
            z=z0
            r=i*20
            g=i*15
            b=i*20
            image.putpixel((x,y),(r,g,b))
image
```

#### Tercer Fractal
![Tercer Fractal - Conjunto de Julia](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/julia%203.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=cos(z)+20+c" />
<img src="https://latex.codecogs.com/svg.latex?\Large&space;c=(1+i)" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-2
xb=2
ya=-2
yb=2
maxit=30

def f(z):
    return np.cos(z)+20+complex(1,1)

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            z0=f(z)
            if abs(z)>1000:
                break
            z=z0
            r=i*10
            g=i*11
            b=i*20
            image.putpixel((x,y),(r,g,b))
image
```

#### Cuarto Fractal
![Cuarto Fractal - Conjunto de Julia](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/julia%204.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=sen(z)+12+c" />
<img src="https://latex.codecogs.com/svg.latex?\Large&space;c=(0,3+0,3i)" />

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
import numpy as np
import sympy as spp
from ipywidgets import interact, interactive, fixed, interact_manual, widgets
from sympy.parsing.sympy_parser import parse_expr
from PIL import Image

imgx=600
imgy=600
image=Image.new("RGB",(imgx,imgy))
image.putpixel((100,100),(255,255,255))

xa=-2
xb=2
ya=-2
yb=2
maxit=30

def f(z):
    return np.sin(z)+12+complex(0.3,0.3)

for y in range (imgy):
    zy=y*(yb-ya)/(imgy-1)+ya
    for x in range (imgx):
        zx=x*(xb-xa)/(imgx-1)+xa
        z=complex(zx,zy)
        for i in range (maxit):
            z0=f(z)
            if abs(z)>1000:
                break
            z=z0
            r=i*50
            g=i*20
            b=i*30
            image.putpixel((x,y),(r,g,b))
image
```

### Curva de Koch
La curva de Koch fue introducida por Helge von Koch en 1904. Este monstruo matemático posee características ciertamente desconcertantes:
- En esta curva no es posible trazar una tangente en ningún punto de su perímetro.
- La longitud entre dos puntos de su perímetro es infinita.
- En relación al copo de nieve de Koch, comprobaremos como una curva de longitud (perímetro) infinita encierra un área finita.

A continuación, pasamos a describir su construcción: 
1. Consideramos un segmento de recta, de longitud n.

![1](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/1.JPG)

2. Reemplazamos el intervalo central de longitud 1/3. por dos segmentos de la misma longitud formando un ángulo de 60 grados.

![2](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/2.JPG)

3. En cada uno de los 4 intervalos que se han formado, repetimos la operación.

![3](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/3.JPG)

4. Así sucesivamente. La curva de Koch es el límite de este proceso innfinito.

![4](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/4.JPG)

La dimensión de Hausdorff de la curva de Koch es s = log(4)/log(3) = 1.26185, ya que es autosemejante con cuatro partes semejantes al total, a escala de un 1/3.

A continuación veremos algunos ejemplos:

#### Primer Fractal
![Iterado 1](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/iterada%201.png)

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.figure as fg
from matplotlib import cm 
import numpy as np 
from PIL import Image
from math import sin, cos, pi, atan2
from pylab import *

def copoVonKoch(lado, n):
    x_vertice1 = 0
    y_vertice1 = 0
 
    x_vertice2 = lado * cos(2 * pi / 3)
    y_vertice2 = lado * sin(2 * pi / 3)
 
    x_vertice3 = lado * cos(pi / 3)
    y_vertice3 = lado * sin(pi / 3)
 
    (x_vertice1, y_vertice1, x_vertice2, y_vertice2, n)
    curvaVonKoch(x_vertice2, y_vertice2, x_vertice3, y_vertice3, n)
    curvaVonKoch(x_vertice3, y_vertice3, x_vertice1, y_vertice1, n)
    return

def curvaVonKoch(xi, yi, xf, yf, n):
    if n == 0:
        plot([xi, xf], [yi, yf], lw=1.0, color='r')
    elif n > 0:
        x1 = xi + (xf - xi) / 3.0
        y1 = yi + (yf - yi) / 3.0

        x3 = xf - (xf - xi) / 3.0
        y3 = yf - (yf - yi) / 3.0

        radio = hypot(x3 - x1, y3 - y1)
        alpha = atan2((y3 - y1), (x3 - x1))
        alpha += pi / 3.0
        x2 = x1 + radio * cos(alpha)
        y2 = y1 + radio * sin(alpha)

        curvaVonKoch(xi, yi, x1, y1, n - 1)
        curvaVonKoch(x1, y1, x2, y2, n - 1)
        curvaVonKoch(x2, y2, x3, y3, n - 1)
        curvaVonKoch(x3, y3, xf, yf, n - 1)
    return
curvaVonKoch(-1, 2, 1, 1, 5)
```

#### Primer Fractal
![Iterado 2](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/Ite.png)

##### Algoritmo de creación 
```
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.figure as fg
from matplotlib import cm 
import numpy as np 
from PIL import Image
from math import sin, cos, pi, atan2
from pylab import *

def copoVonKoch(lado, n):
    x_vertice1 = 0
    y_vertice1 = 0
 
    x_vertice2 = lado * cos(2 * pi / 3)
    y_vertice2 = lado * sin(2 * pi / 3)
 
    x_vertice3 = lado * cos(pi / 3)
    y_vertice3 = lado * sin(pi / 3)
 
    (x_vertice1, y_vertice1, x_vertice2, y_vertice2, n)
    curvaVonKoch(x_vertice2, y_vertice2, x_vertice3, y_vertice3, n)
    curvaVonKoch(x_vertice3, y_vertice3, x_vertice1, y_vertice1, n)
    return

def curvaVonKoch(xi, yi, xf, yf, n):
    if n == 0:
        plot([xi, xf], [yi, yf], lw=1.0, color='g')
    elif n > 0:
        x1 = xi + (xf - xi) / 3.0
        y1 = yi + (yf - yi) / 3.0

        x3 = xf - (xf - xi) / 3.0
        y3 = yf - (yf - yi) / 3.0

        radio = hypot(x3 - x1, y3 - y1)
        alpha = atan2((y3 - y1), (x3 - x1))
        alpha += pi / 3.0
        x2 = x1 + radio * cos(alpha)
        y2 = y1 + radio * sin(alpha)

        curvaVonKoch(xi, yi, x1, y1, n - 1)
        curvaVonKoch(x1, y1, x2, y2, n - 1)
        curvaVonKoch(x2, y2, x3, y3, n - 1)
        curvaVonKoch(x3, y3, xf, yf, n - 1)
    return
copoVonKoch(2, 4)
```

### 
