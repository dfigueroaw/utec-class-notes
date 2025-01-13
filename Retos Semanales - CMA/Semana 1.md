$$I=\int_0^\frac{\pi}{2}\frac{\sqrt{\sin x}}{\sqrt{\sin x}+\sqrt{\cos x}}dx$$
### ¿Qué es la regla de King?
Una propiedad geométrica muy interesante de algunas integrales es la **simetría**. La regla de King nos permite aprovechar la simetría de las integrales para simplificar problemas difíciles de resolver. Para una función continua en un intervalo cerrado $[a, b]$ se cumple:
$$\int_a^bf(x)dx=\int_a^bf(a+b-x)dx$$
**¿De donde viene esto?**
Para demostrar esta propiedad podemos realizar un cambio de variable
$$x=a+b-u, \quad dx=-du$$
Procedemos a cambiar los límites de integración
$$x=a\rightarrow u=b$$
$$x=b\rightarrow u=a$$
Y la integral finalmente queda
$$\int_a^bf(x)dx=-\int_b^af(a+b-u)du=\int_a^bf(a+b-u)du=\int_a^bf(a+b-x)dx$$



Realizamos un cambio de variable
$$x=\frac{\pi}{2}-\theta, \quad dx=-d\theta$$
Cambiando los límites de integración
$$x=0\rightarrow\theta=\frac{\pi}{2}$$
$$x=\frac{\pi}{2}\rightarrow\theta=0$$
Entonces