```ad-definition
Una ecuación diferencial de la forma

$$\frac{dy}{dx} = f(y)$$

libre de la variable independienten es denominada autónoma.
```

Como veremos a continuación, las ecuaciones diferenciales de primer orden autónomas cumplen con muchas propiedades interesantes debido a su forma particular en la que la función que se tiene en términos de la variable independiente es igual a su derivada.
## Puntos críticos

```ad-theorem
Si $f(c) = 0$, entonces $c$ es un punto crítico, punto de equilibrio o punto estacionario. Si $c$ es un punto crítico, entonces tenemos $0 = f(c) = 0$, por lo tanto, $y(x) = c$ es una solución, denominada **solución de equilibrio**.
```

Primero, definimos la región $\mathcal{R}$ como el intervalo sobre el cual estamos considerando la función $f(y)$ y sus puntos críticos.  Cabe aclarar que $\mathcal{R}$ no siempre será igual a $\mathbb{R}$, puesto que esto únicamente ocurrirá cuando el dominio de $f(y)$ sean todos los números reales.

Según la región $R$, podemos graficar un [[II. Campos direccionales|campo direccional]] que describa el comportamiento de la ecuación diferencial en distintos puntos del plano.

Según la cantidad de soluciones de equilibrio, podemos subdividir $\mathcal{R}$ en múltiples subregiones. Diremos que si $c_1, c_2, \dots, c_n$ son puntos críticos de $f(y)$, y además $c_1<c_2<\dots<c_n$, entonces las soluciones de equilibrio $y(x)=c_1, y(x)=c_2, \dots, y(x)=c_n$ dividen a $\mathcal{R}$ en subregiones.

Por inducción, podemos ver que si $f$ tiene $n$ soluciones de equilibrio distintas, entonces $\mathcal{R}$ esta dividido en $n+1$ subregiones.

## Teoremas
A continuación presentaremos algunos de los teoremas relacionados a campos direccionales de ecuaciones diferenciales autónomas. Las demostraciones proporcionadas estarán principalmente orientadas a llegar a los resultados desde la idea intuitiva detrás de cada teorema.

```ad-theorem
Si $f(y)$ se encuentra en una subregión de $\mathcal{R}$ en la cual es continua, entonces $f(y)$ no puede cambiar de signo en dicha subregión.
```
### Demostración
Recordemos que para que una ecuación diferencial de primer orden sea considerada autónoma, debe cumplir que $\frac{dy}{dx} = f(y)$, lo cual nos brinda la siguiente información de la función $f(y)$
- Cuando $f(c)$ es positiv0, también lo es $\frac{dy}{dx}$
- Cuando $f(c)$ es negativo, también lo es $\frac{dy}{dx}$
- Cuando $f(c)$ es $0$, entonces sabemos que $c$ es punto crítico de $f$, y por lo tanto divide a $f$ en dos subregiones.
Como empezamos suponiendo que $f$ es continua, para que $f(y)$ cambie de signo tendría que necesariamente pasar por $f(y)=0$, lo cual delimita una subregión del campo direccional e implicaría que $f$ tendría que cambiar de subregión.

```ad-theorem
Si el punto $(x_0, y_0)$ se encuentran en una de las subregiones de $\mathcal{R}$ en la cual $f(y)$ es continua, entonces la solución $y(x)$ que pasa por $(x_0, y_0)$ permanecerá en la misma subregión.
```
### Demostración
Como sabemos que $f$ necesariamente cumple $\frac{dy}{dx}=f(y)$, podrían ocurrir dos situaciones
- Si consideramos la solución $y(x)=c$, en la que $c$ es una solución de equilibrio de la ecuación diferencial, entonces $\frac{dy}{dx}=0$, por lo tanto la solución $y(x)$ se mantendría constante y por ende se mantendría en la misma subregión.
- Caso contrario, si tomamos como la solución a la ecuación diferencial una solución distinta a la solución de equilibrio, por el teorema anterior, podemos garantizar que la función será necesariamente o monótona creciente o monótona decreciente en dicha subregión.
Ahora, para demostrar que $y(x)$ siempre se mantiene en la misma subregión de $\mathcal{R}$, nos centraremos únicamente en el segundo caso, pues el primero ya quedó demostrado. 

Primero, empezamos suponiendo que existe el caso en el que $f$ si pudiera cambiar de subregión. En tal caso, el punto $(x_0, y_0)$ se encuentra inicialmente en una subregión de $\mathcal{R}$ en la cual $f$ es monótona. Sin embargo, por el anterior teorema, sabemos que para pasar a otra región necesariamente tenemos que pasar

```ad-theorem
Puesto que $\frac{dy}{dx} = f(y)$ es o positivo o negativo en cada una de las subregiones de $\mathcal{R}$, una solución $y(x)$ es **monótona**.
```
### Demostración
Del teorema anterior, sabemos que $f(y)$ no puede cambiar de signo en una subregión.

```ad-theorem
Si $y(x)$ está acotado por $c_1$ $(y(x) < c_1)$, la gráfica de $y(x)$ se aproximará a $y(x) = c_1$. Si $c_1 < y(x) < c_2$, se aproximará a $y(x) = c_1$ y $y(x) = c_2$. Si $c_2 < y(x)$, se aproximará a $y(x) = c_2$.
```


## Atractores y repulsores

