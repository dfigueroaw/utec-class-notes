## Variable aleatoria
ES la representación numérica de un experimento aleatorio.
Puede ser:
- Variable aleatoria **discreta**: Toma valores enteros
- Variable aleatoria **continua**: Toma valores en el campo de los números reales

>[!example]
>Se lanzan dos **monedas**. Se define la variable aleatoria $X$ como el número de caras obtenidas.
>
>Representar en función de $X$, la probabilidad de obtener **al menos una cara**
>
>**Solución**:
>
>$\Omega=\{CC, CS, SC, SS\}$
>
>$X=\{0, 1, 2\}$
>
>$P(X\geq1)=P(X>0)=\frac{3}{4}$
>

## Distribución Binomial
**Se debe cumplir**:
- Una repetición de $n$ ensayos
- El resultado de cada ensayo es independiente
- Existe una probabilidad de **éxito** y **fracaso**

La formula para calcular la distribución binomial es:

$$P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}$$

Donde $p$ es la probabilidad de éxito y $n$ es el número de ensayos. Adicionalmente que $q$ es la probabilidad de fracaso, de donde se deduce que $p+q=1$.

Además, para una variable $X$ que tiene una distribución binomial se cumple que
- Media ($\mu$)=$np$
- Varianza = $npq$
- CV = $\frac{\sqrt{npq}}{\mu}$

>[!example]
>La probabilidad de que un paciente quede hospitalizado luego de entrar por emergencia es 0.78. Hallar la probabilidad que de un total de 10 pacientes 8 pacientes queden hospitalizados.
>
>**Solución**:
>
>$X$: Número de pacientes que son hospitalizados luego de acudir a emergencia.
>
>$P(X=8)=\binom{10}{8}(0.78)^8(0.22)^2=29.84\%$
