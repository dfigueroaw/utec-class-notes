Existen dos tipos fundamentales de regresión lineal.

### Regresión lineal simple
Se describe mediante la función
$$y=mx+b$$
Nos ayuda para obtener información sobre la relación entre dos variables. La pendiente (el termino $m$) nos indica distintas cosas
- Para $m$ negativo, podemos suponer que mediante la variable $x$ aumenta, entonces la variable $y$ también tiende a crecer. En este caso, se dice que es **correlación directa**.
- Para $m$ positivo, podemos suponer que mediante la variable $x$ aumenta, entonces la variable $y$ tiende a decrecer. En este caso, se dice que es **correlación inversa**.

### Coeficiente de correlación
El coeficiente de correlación $r$ es un valor $-1\leq r\leq 1$ que nos indica el nivel de correlación entre ambas variables.
- Si $|r|<0.3$ entonces la correlación entre ambas variables es baja
- Si $0.3\leq |r|<0.6$ entonces la correlación es media/regular/moderada
- Si $0.6<|r|$ entonces la correlación es alta

Adicionalmente, el coeficiente de determinación $R²=r²$ es un coeficiente similar al anterior, el cual toma un valor entre $0\leq R²\leq 1$. Se dice que si $R²\geq 0.7$, entonces se afirma que es un **modelo confiable**.

En resumen:
- $R^2$: Mide en que medida la variable dependiente $y$ es explicada por el modelo de regresión ajustado
- $r$: Mide el grado de asociación entre dos variables numéricas

>[!note]
>La variable $x$ suele llamarse la variable explicativa, mientras que la variable $y$ se denomina dependiente.

En **r**, la función `lm(y~x)` nos retorna tanto el intercepto de la función lineal (el valor de $b$) como la pendiente $m$. Adicionalmente, `cor(x, y)` nos retorna el **coeficiente de correlación**.

Para graficar la regresión lineal, usamos primero la función `plot(y~x)` y luego para mostrar la recta usamos `abline(lm(y~x), col="red")` para crear una recta con la recta obtenida por nuestra regresión

Si queremos la correlación de una data que no esta limpia, usaremos la función `cor(x, y, use="complete.obs")`, pues queremos contar únicamente las observaciones que contengan $x$ e $y$.
