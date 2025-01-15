```ad-definition
Una ecuación diferencial de la forma

$$\frac{dy}{dx} = f(y)$$

libre de la variable independienten es denominada autónoma.
```
## Puntos críticos

```ad-theorem
Si $f(c) = 0$, entonces $c$ es un punto crítico, punto de equilibrio o punto estacionario. Si $c$ es un punto crítico, entonces tenemos $0 = f(c) = 0$, por lo tanto, $y(x) = c$ es una solución, denominada **solución de equilibrio**.
```

Primero, definimos la región $\mathcal{R}$ como el intervalo sobre el cual estamos considerando la función $f(y)$ y sus puntos críticos.  Cabe aclarar que $\mathcal{R}$ no siempre será igual a $\mathbb{R}$, puesto que esto únicamente ocurrirá cuando el dominio de $f(y)$ sean todos los números reales.

Según la región $R$, podemos graficar un [[II. Campos direccionales|campo direccional]] que describa el comportamiento de la ecuación diferencial en distintos puntos del plano.

Según la cantidad de soluciones de equilibrio, podemos subdividir $\mathcal{R}$ en múltiples subregiones. Diremos que si $c_1, c_2, \dots, c_n$ son puntos críticos de $f(y)$, y además $c_1<c_2<\dots<c_n$, entonces las soluciones de equilibrio $y(x)=c_1, y(x)=c_2, \dots, y(x)=c_n$ dividen a $\mathcal{R}$ en subregiones.

Por inducción, podemos ver que si $f$ tiene $n$ soluciones de equilibrio distintas, entonces $\mathcal{R}$ esta dividido en $n+1$ subregiones.

### Teoremas
A continuación presentaremos algunos de los teoremas relacionados a campos direccionales de ecuaciones diferenciales autónomas. Las demostraciones proporcionadas estarán orientadas más a la idea intuitiva que a formalizar estos conceptos.

```ad-theorem
Si $(x_0, y_0)$ se encuentra en una de las subregiones de $\mathcal{R}$ entonces la solución $y(x)$ que pasa por $(x_0, y_0)$ permanecerá en la misma subregión.
```

```ad-theorem
Por continuidad de $f$, $f(y)$ no puede cambiar de signo en una subregión.
```
### Demostración
Recordemos que para que una ecuación diferencial de primer orden sea considerada autónoma, debe cumplir que $\frac{dy}{dx} = f(y)$, lo cual nos brinda la siguiente información de la función $f(y)$
- Cuando $f(c)$ es positiv0 también lo es $\frac{dy}{dx}$
- Cuando $f(c)$ es negativo también lo es $\frac{dy}{dx}$
- Cuando $f(c)$ es $0$, entonces sabemos que $c$ es punto crítico  de $f$ y por lo tanto divide a $f$ en dos subregiones.
Como empezamos suponiendo que $f$ es continua, para que $f(y)$ cambie de signo tendría que necesariamente pasar por $f(y)=0$, lo cual delimita una subregión del campo direccional.

```ad-theorem
Puesto que $\frac{dy}{dx} = f(y)$ es o positivo o negativo en $R_i$, una solución y(x) es **monótona**.
```

```ad-theorem
Si $y(x)$ está acotado por $c_1$ $(y(x) < c_1)$, la gráfica de $y(x)$ se aproximará a $y(x) = c_1$. Si $c_1 < y(x) < c_2$, se aproximará a $y(x) = c_1$ y $y(x) = c_2$. Si $c_2 < y(x)$, se aproximará a $y(x) = c_2$.
```

## Atractores y repulsores

