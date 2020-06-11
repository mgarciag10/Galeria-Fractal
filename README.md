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

## Tipos de Fractales 
Algunos ejemplos de fractales son:

### Conjuntos de Newton
El fractal de Newton es una curiosa creación basado en la aplicación del método de Newton para la resolución de sistemas de ecuaciones no lineales. El algoritmo es eficiente para encontrar aproximaciones de los ceros o raíces de una función real. También puede ser usado para encontrar el máximo o mínimo de una función, encontrando los ceros de su primera derivada.

La idea de este método es la siguiente: se comienza con un valor razonablemente cercano al cero (denominado punto de arranque), entonces se reemplaza la función que estamos tratando por la recta tangente en ese valor, se iguala a cero y se despeja. Este cero será, generalmente, una aproximación mejor a la raíz de la función. Luego, se aplican tantas iteraciones como se deseen hasta que el método de una solución adecuada. Cabe destacar que es posible que el método diverja en determinadas circunstancias que pueden depender de la elección del punto inicial.

Además es responsabilidad nuestra la elección de un buen test de parada, aunque dicho test podría basarse simplemente en el número de iteraciones realizadas.

<img src="https://latex.codecogs.com/svg.latex?\Large&space&center;x_{n+1}=x_{n}-\dfrac{f(x_{n})}{f'(x_{n})}" />

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
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=(z^{2}-4)(z^{3]-10)+2" />

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

#### Primer Fractal
![Primer Fractal - Conjunto de Julia](https://raw.githubusercontent.com/mgarciag10/Galeria-Fractal/master/julia%201.png)
##### Función
<img src="https://latex.codecogs.com/svg.latex?\Large&space;f(z)=z^{4}" />

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
