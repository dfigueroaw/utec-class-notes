## Problema 0
**Enunciado**: Determinar para que valores de $x$ e $y$ se tiene que el número $42x4y$ es divisible por 42.

Solución:

Podemos reescribir el número $42x4y$ como la suma

$$42000 + x4y$$

Sabemos que $42 | 42000$, por lo tanto podemos reducir el problema a únicamente comprobar los $x$ e $y$ los cuales cumplen que $x4y$ es divisible por 42.

Para que un número sea divisible por 42, el número tiene que ser divisible por 2, 3 y 7.

Para la divisibilidad entre 2, necesitamos garantizar que el número sea par, es decir, el último dígito debe ser múltiplo 2. De esto, sabemos que

$$y\in\{0, 2, 4, 6, 8\}$$

Para la divisibilidad entre 3, necesitamos garantizar que la suma de los dígitos del número sea múltiplo de 3. De esto, obtenemos...

$$x+4+y=3k$$

$$x+y=3k+2$$

Para la divisibilidad entre 7, similar a como hicimos al inicio, podemos descomponer el número en partes

$$x4y=100x+40+y$$

Como sabemos que $7|x4y$, entonces...

$$100x+40+y=7k$$

$$(98x+35)+2x+5+y=7k$$

Como podemos ver, $98x+35$ es divisible entre 7, entonces...

$$2x+y+5=7k$$

$$2x+y=7k+2$$

Sabemos que tanto $2x$ como $y$ son pares, por ende el lado izquierdo de la igualdad siempre será par. Del lado derecho, vemos que $7k+2$ es par únicamente cuando $k$ es par, por lo tanto, podemos reescribir la expresión como...

$$2x+y=14k+2$$

Considerando que $x$ e $y$ son números naturales entre 0 y 9, sabemos que el valor máximo que puede tomar $2x+y$ es 27. De esto, podemos deducir que en la ecuación solo nos quedan dos posibles casos: $k=0$ y $k=1$.

Empezando para $k=0$

$$2x+y=2$$

Los pares que cumplen esto son $(0, 2)$ y $(1, 0)$. Si bien el par $(1, 0)$ cumple la divisibilidad por 7, no cumple la condición que planteamos para la divisibilidad por 3, por lo que quedaría descartado. Para el par $(2, 0)$ cumple con todos los criterios de divisibilidad, y podemos ver que 42042 es divisible por 42, por lo que tenemos una primera solución.

Ahora, para $k=1$

$$2x+y=16$$

Vemos que los pares que cumplen son $(4, 8)$, $(5, 6)$, $(6, 4)$, $(7, 2)$ y $(8, 0)$. Si bien todos cumplen la primera condición de divisibilidad por 2, vemos que solo $(5, 6)$ y $(8, 0)$ cumplen la condición para garantizar la divisibilidad por 3, y efectivamente vemos que 42546 y 42840 son divisibles por 42. Con esto, finalmente obtenemos todas las soluciones

$$\{(2, 0), (5, 6), (8, 0)\}$$

## Problema 1
**Enunciado**: Calcular los últimos tres dígitos de $7^{2025}$.

Empezaremos desarrollando las primeras potencias de 7 con el fin de notar un posible patrón. Como nos interesa encontrar un patrón específicamente en los tres últimos dígitos, nos fijaremos únicamente en estos tres usando el operador módulo a la hora de aplicar las potencias.

$7^{0}\equiv1\pmod{1000}$
$7¹\equiv7\pmod{1000}$
$7²\equiv49\pmod{1000}$
$7^3\equiv343\pmod{1000}$
$7⁴\equiv401\pmod{1000}$
$7⁵\equiv807\pmod{1000}$
$7⁶\equiv649\pmod{1000}$
$7⁷\equiv543\pmod{1000}$
$7⁸\equiv801\pmod{1000}$
$7⁹\equiv607\pmod{1000}$

De aquí podemos notar dos patrones. Primero, vemos que los dos últimos dígitos repiten un patrón de 07 -> 49 -> 43 -> 01, repitiéndose indefinidamente en ciclos de 4. Además, notamos que partiendo de $n=1$, cada vez que el exponente aumenta en 4 la cifra de las centenas disminuye en 2. Para visualizar esta última hipótesis, podemos desarrollar algunas potencias más.

$7^{13}\equiv407\pmod{1000}$
$7^{17}\equiv207\pmod{1000}$
$7^{21}\equiv7\pmod{1000}$

Podemos efectivamente notar un patrón en los números al realizar estos aumentos de cuatro. Sin embargo, podemos ver que después de repetir este proceso cinco veces, cuando llegamos a $n=21$, volvemos a obtener el mismo resultado que para $n=1$. De esto, podemos ver que probablemente existe una relación entre los $n$ con diferencias de 20. Para comprobar esto, podemos plantear un par de casos más.

$7^{20}\equiv1\pmod{1000}$
$7^{21}\equiv7\pmod{1000}$
$7^{22}\equiv49\pmod{1000}$

Podemos notar que después de 20 dígitos, empieza a ocurrir cierto patrón en las congruencias. Nuestra hipótesis será que los tres últimos dígitos de una potencia de 7 serán los mismos cada vez que el exponente aumente en saltos de 20. Matemáticamente, queremos probar que $7^{n+20k}\equiv7^{n}\pmod{1000}$.

Empezamos reescribiendo el lado izquierdo de la igualdad

$7^{n}7^{20k}\equiv7^{n}\pmod{1000}$

Como $7^n$ y 1000 son coprimos, podemos plantear que existe un inverso multiplicativo modular de ${7^n}$. De esto, obtenemos...

$7^{20k}\equiv1\pmod{1000}$

$(7^{20})^k\equiv1\pmod{1000}$

Sabemos que si $7^{20}\equiv1\pmod{1000}$, entonces $(7^{20})^k\equiv1\pmod{1000}$. Comprobando para $7^{20}$...

$7^{20}\equiv1\pmod{1000}$

Lo cual como vimos al inicio es verdad, por lo tanto nuestra hipótesis es verdadera. Al inicio vimos que para $n=5$ tenemos que $7⁵\equiv807\pmod{1000}$, usando la propiedad que acabamos de demostrar y tomando $k=101$, entonces podemos ver que $7^{2025}\equiv807\pmod{1000}$. Por lo tanto, podemos ver que los tres últimos dígitos de $7^{2025}$ son **807**.