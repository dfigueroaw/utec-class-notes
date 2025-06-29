Vamos a desarrollar el **algoritmo de backpropagation** paso a paso y con rigor matemático. Usaremos una red neuronal **feedforward** completamente conectada con varias capas.

## 🧮 Notación general

Para cada capa $l$:

- $a^{[l]}$: activaciones de la capa $l$ (vector columna)
- $z^{[l]}$: entrada lineal de la capa $l$:

  $$
  z^{[l]} = W^{[l]} a^{[l-1]} + b^{[l]}
  $$

- $W^{[l]}$: matriz de pesos de forma $(n_l \times n_{l-1})$
- $b^{[l]}$: vector de bias
- $\sigma^{[l]}$: función de activación
- $\hat{y} = a^{[L]}$: salida de la red
- $y$: etiqueta verdadera
- $\mathcal{L}(\hat{y}, y)$: función de pérdida
- $L$: número total de capas
- $m$: número de ejemplos en el batch

## 🚀 Objetivo

Calcular los **gradientes del costo** con respecto a todos los **parámetros entrenables**:

$$
\frac{\partial \mathcal{L}}{\partial W^{[l]}}, \quad \frac{\partial \mathcal{L}}{\partial b^{[l]}} \quad \text{para todo } l
$$

Usamos la **regla de la cadena** hacia atrás desde la salida.

## 🔁 Forward Propagation

1. Inicializa $a^{[0]} = x$
2. Para cada capa $l = 1$ hasta $L$:

   $$
   z^{[l]} = W^{[l]} a^{[l-1]} + b^{[l]}
   $$

   $$
   a^{[l]} = \sigma^{[l]}(z^{[l]})
   $$

3. La salida es $\hat{y} = a^{[L]}$

## 🔄 Backward Propagation

### 1. Cálculo del error en la capa de salida

$$
\delta^{[L]} = \nabla_{a^{[L]}} \mathcal{L} \circ \sigma'^{[L]}(z^{[L]})
$$

Donde:

- $\nabla_{a^{[L]}} \mathcal{L}$ es la derivada de la pérdida respecto a la activación
- $\circ$ es el producto elemento a elemento
- $\sigma'$ es la derivada de la activación

### 2. Propagación hacia atrás

Para $l = L-1, L-2, ..., 1$:

$$
\delta^{[l]} = \left( (W^{[l+1]})^T \delta^{[l+1]} \right) \circ \sigma'^{[l]}(z^{[l]})
$$

### 3. Cálculo de los gradientes

$$
\frac{\partial \mathcal{L}}{\partial W^{[l]}} = \delta^{[l]} (a^{[l-1]})^T
$$

$$
\frac{\partial \mathcal{L}}{\partial b^{[l]}} = \delta^{[l]}
$$

## 🧠 Ejemplo con MSE y Sigmoid

Supongamos:

$$
\mathcal{L}(\hat{y}, y) = \frac{1}{2} \|\hat{y} - y\|^2
$$

Entonces:

$$
\nabla_{a^{[L]}} \mathcal{L} = \hat{y} - y
$$

$$
\delta^{[L]} = (\hat{y} - y) \circ \sigma'^{[L]}(z^{[L]})
$$

$$
\delta^{[l]} = \left( (W^{[l+1]})^T \delta^{[l+1]} \right) \circ \sigma'^{[l]}(z^{[l]})
$$

## 📦 Algoritmo resumido

1. **Forward pass**: calcula todos los $z^{[l]}$ y $a^{[l]}$
2. **Backward pass**:
   - Calcula $\delta^{[L]}$
   - Propaga $\delta^{[l]}$
   - Calcula:

     $$
     \frac{\partial \mathcal{L}}{\partial W^{[l]}}, \quad \frac{\partial \mathcal{L}}{\partial b^{[l]}}
     $$

3. **Gradient descent**:

   $$
   W^{[l]} := W^{[l]} - \eta \cdot \frac{\partial \mathcal{L}}{\partial W^{[l]}}
   $$

   $$
   b^{[l]} := b^{[l]} - \eta \cdot \frac{\partial \mathcal{L}}{\partial b^{[l]}}
   $$
