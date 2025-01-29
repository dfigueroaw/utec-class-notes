## Problema 0
**Enunciado**: Determinar para que valores de $x$ e $y$ se tiene que el número $42x4y$ es divisible por 42.

Solución:

Podemos reescribir el número $42x4y$ como la suma

$$42000 + x4y$$

Sabemos que $42 | 42000$, por lo tanto podemos reducir el problema a únicamente comprobar los $x$ e $y$ los cuales cumplen que $x4y$ es divisible por 42.

Para que un número sea divisible por 42, el número tiene que ser divisible por 2, 3 y 7.

Para la divisibilidad por 2, necesitamos garantizar que el número sea par, es decir, el último dígito debe ser múltiplo 2. De esto, sabemos que

$$y\in\{0, 2, 4, 6, 8\}$$

Para la divisibilidad por 3, necesitamos garantizar que la suma de los dígitos del número sea múltiplo de 3. De esto, obtenemos...

$$x+4+y=3k$$

$$x+y=3k+2$$

