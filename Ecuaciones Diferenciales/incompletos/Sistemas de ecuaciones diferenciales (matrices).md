Temporalmente, solo se describirán las formas de las soluciones, más no se brindara ninguna demostración.

Para un sistema $X'=AX$, si la matriz $A$ tiene $n$ eigenvalores **diferentes** la solución general estará dada por:

$$X=c_1K_1e^{\lambda_1t}+c_2K_2e^{\lambda_2t}+\dots+c_nK_ne^{\lambda_nt}$$

Donde $K_i$ es el eigenvector asociado al eigenvalor $\lambda_i$.

---
En caso existan eigenvalores repetidos, tenemos tres casos:
1. Se tienen $n$ eigenvectores linealmente independientes. En tal caso, simplemente se reemplazan los $K_i$ de los eigenvalores repetidos por cada eigenvector generado por $\lambda_i$.

Los dos últimos casos particulares son los más complicados. Se analiza para $n=3$.

2. En caso un eigenvalor $\lambda$ con multiplicidad 2 solo tiene un eigenvector $K$ asociado, entonces la solución general está dada por:

$$X=c_1Ke^{\lambda t}+c_2\left(Kte^{\lambda t}+Pe^{\lambda t}\right)+\dots$$

$P$ se obtiene de resolver el sistema

$$(A-\lambda I_n)P=K$$

3. En caso un eigenvalor $\lambda$ con multiplicidad 3 solo tiene un eigenvector $K$ asociado, entonces la solución general está dada por:

$$X=c_1Ke^{\lambda t}+c_2\left(Kte^{\lambda t}+Pe^{\lambda t}\right)+c_3\left(K\frac{t^2}{2}e^{\lambda t}+Pte^{\lambda t}+Qe^{\lambda t}\right)+\dots$$

$P$ y $Q$ se obtienen de resolver los sistemas

$$(A-\lambda I_n)P=K$$

$$(A-\lambda I_n)Q=P$$
