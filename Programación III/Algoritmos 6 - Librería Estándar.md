# 🧩 Funciones de conjuntos y fusión en C++

Estas funciones trabajan sobre **dos rangos ordenados** y producen una salida que también es un rango ordenado. Son útiles para operaciones de teoría de conjuntos. Si el rango no está ordenado, primero usa `std::sort`.

| Función           | ¿Qué hace? |
|--------------------|-----------|
| `merge`            | Fusiona dos rangos ordenados en uno solo. |
| `set_union`        | Unión de conjuntos: todos los elementos, sin duplicar. |
| `set_difference`   | Diferencia de conjuntos: elementos del primer rango que no están en el segundo. |

> ⚠️ Todos los rangos de entrada deben estar **ordenados** según el mismo criterio.

---

## 🔗 `std::merge`

**Descripción:** Combina dos secuencias ordenadas en una sola secuencia también ordenada.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a{1, 3, 5};
    std::vector<int> b{2, 4, 6};
    std::vector<int> resultado(a.size() + b.size());

    // Ejemplo 1: Fusión de a y b
    std::merge(a.begin(), a.end(), b.begin(), b.end(), resultado.begin());

    for (int x : resultado)
        std::cout << x << " "; // Resultado: 1 2 3 4 5 6
}
````

---

## 🤝 `std::set_union`

**Descripción:** Devuelve la unión de dos conjuntos ordenados, sin duplicar elementos comunes.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a{1, 2, 4};
    std::vector<int> b{2, 3, 4};
    std::vector<int> resultado(a.size() + b.size());

    // Ejemplo 1: Unión de conjuntos
    auto it = std::set_union(a.begin(), a.end(), b.begin(), b.end(), resultado.begin());
    resultado.resize(it - resultado.begin());

    for (int x : resultado)
        std::cout << x << " "; // Resultado: 1 2 3 4
}
```

---

## ➖ `std::set_difference`

**Descripción:** Devuelve los elementos del primer rango que no están en el segundo.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a{1, 2, 3, 4, 5};
    std::vector<int> b{2, 4, 6};
    std::vector<int> resultado(a.size());

    // Ejemplo 1: Diferencia A - B
    auto it = std::set_difference(a.begin(), a.end(), b.begin(), b.end(), resultado.begin());
    resultado.resize(it - resultado.begin());

    for (int x : resultado)
        std::cout << x << " "; // Resultado: 1 3 5
}
```
