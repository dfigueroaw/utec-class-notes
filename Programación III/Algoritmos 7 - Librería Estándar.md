# 🔍 Búsquedas avanzadas en C++ STL

Estas funciones buscan elementos o rangos en un contenedor **ordenado**. Son rápidas (`O(log n)`) porque utilizan **búsqueda binaria**.

| Función           | ¿Qué hace? |
|-------------------|------------|
| `binary_search`   | Verifica si un elemento existe. |
| `lower_bound`     | Devuelve el primer elemento que **no es menor** que el valor buscado. |
| `equal_range`     | Devuelve el rango de todos los elementos iguales al valor buscado. |

> ⚠️ Estas funciones **requieren que el rango esté previamente ordenado** según el mismo criterio de comparación.

---

## ✅ `std::binary_search`

**Descripción:** Devuelve `true` si el elemento buscado está presente.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 3, 4, 6, 8};
    
    // Ejemplo 1: Buscar el 4
    bool existe = std::binary_search(v.begin(), v.end(), 4);
    
    std::cout << std::boolalpha << existe << "\n"; // Resultado: true
}
````

---

## 🔽 `std::lower_bound`

**Descripción:** Devuelve un iterador al **primer elemento ≥ valor** buscado.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 4, 4, 5, 6};

    // Ejemplo 1: Buscar primer elemento ≥ 4
    auto it = std::lower_bound(v.begin(), v.end(), 4);

    std::cout << "Posición: " << (it - v.begin()) << "\n"; // Resultado: 2
}
```

---

## 🔁 `std::equal_range`

**Descripción:** Devuelve un par de iteradores al rango de todos los elementos iguales al valor.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 4, 4, 4, 5, 6};

    // Ejemplo 1: Rango de elementos con valor 4
    auto [inicio, fin] = std::equal_range(v.begin(), v.end(), 4);

    std::cout << "Rango: [" << (inicio - v.begin()) << ", " << (fin - v.begin()) << ")\n"; 
    // Resultado: Rango: [2, 5)
}
```
