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

Para empezar, vamos a calcular los 5 primeros valores de $7^n$

7¹=7
7²=49
7³=343
7⁴=2401
7⁵=16807

Vemos que los dos últimos dígitos siguen el patrón de 07 -> 49 -> 43 -> 01, repitiéndose indefinidamente en ciclos de 4. 2025 es un número de la forma $4k+1$, así que queremos demostrar que los dos últimos dígitos de un número de la forma $7^{4k+1}$ son 07, es decir, que podemos escribir el número $7^{4k+1}$ como $7+100n$.

Caso base:
$P(0): 7¹=7+100(0)$

Hipótesis inductiva:
$P(k): 7^{4k+1}=7+100n,\forall k\geq0$

Sabemos que 7⁴=2401. Multiplicando por 2401 ambos lados de la igualdad

$(7^{4k+1})(7⁴)=7^{4(k+1)+1}=(7+100n)2401$

$7^{4(k+1)+1}=16807+(100)(2401)(n)=7+(100)(168)+(100)(2401)(n)$

Hacemos un cambio de variable $m=168+2401n$

$7^{4(k+1)+1}=7+100m\rightarrow P(k+1)$

Lo cual demuestra nuestra proposición inicial. Con esto, vemos que los dos últimos dígitos son 07.

Para la tercera cifra, lo que haremos será seguir desarrollando las potencias de 7 hasta notar un posible patrón. Como nos interesa encontrar un patrón específicamente en el tercer dígitos, haremos el cálculo de únicamente los valores para los 3 primeros dígitos

$7¹\equiv7\pmod{1000}$
$7²\equiv49\pmod{1000}$
$7^3\equiv343\pmod{1000}$
$7⁴\equiv401\pmod{1000}$
$7⁵\equiv807\pmod{1000}$
$7⁶\equiv649\pmod{1000}$
$7⁷\equiv543\pmod{1000}$
$7⁸\equiv801\pmod{1000}$
$7⁹\equiv607\pmod{1000}$
$7^{10}\equiv249\pmod{1000}$
$7^{11}\equiv743\pmod{1000}$
$7^{12}\equiv201\pmod{1000}$
$7^{13}\equiv407\pmod{1000}$

De aquí notamos que partiendo de $n=1$, cada vez que el exponente aumenta en 4 la cifra de las centenas disminuye en 2. Bajo esta suposición, entonces los tres últimos dígitos se repetirían cada 5 veces que el exponente aumenta en 4, es decir, en ciclos de 20.

## Problema 2
**Enunciado**: Determina todos los valores que podría tomar un entero positivo $n$, de modo que se cumpla que $2^n$ sea un divisor de $3^n+1$.

Primero probamos 5 valores para tener una idea del patrón de los términos

$f(n)=\frac{3^{n}+1}{2^n}$
$f(1)=2$
$f(2)=\frac{5}{2}$
$f(3)=\frac{7}{2}$
$f(4)=\frac{41}{8}$
$f(5)=\frac{61}{8}$
...

Vemos que para $n=1$, efectivamente $2^n$ es divisor de $3^n+1$. Por inducción, se va a demostrar que $\forall n\geq2$, $2^n$ no es divisor de $3^n+1$

Caso Base:
$P(2): 4 \nmid 10$

Hipótesis Inductiva:
$P(n): 2^n\nmid 3^n+1$

