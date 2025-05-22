# 🧹 Funciones de eliminación lógica en C++

Estas funciones **no eliminan físicamente** los elementos del contenedor. Solo **reorganizan** el rango, "compactando" los elementos válidos al principio y devolviendo un **iterador al nuevo final** del rango. Para eliminar realmente, se suele usar con `erase`.

| Función       | ¿Qué hace? |
|----------------|------------|
| `remove`       | Reorganiza para eliminar todos los valores iguales al dado. |
| `remove_if`    | Reorganiza para eliminar los que cumplen una condición. |
| `unique`       | Elimina valores duplicados consecutivos. |

> 📌 Después de usar estas funciones, se recomienda aplicar `erase` si se quiere modificar el contenedor.

---

## ❌ `std::remove`

**Descripción:** Reorganiza el rango para eliminar todos los elementos con un valor específico.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 2, 4, 2, 5};

    // Ejemplo 1: Eliminar todos los 2 (lógicamente)
    auto nuevo_fin = std::remove(v.begin(), v.end(), 2);

    // Ejemplo 2: Borrar físicamente
    v.erase(nuevo_fin, v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 1 3 4 5
}
````

---

## ❗ `std::remove_if`

**Descripción:** Reorganiza el rango para eliminar los elementos que cumplen una condición.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 4, 5, 6};

    // Ejemplo 1: Eliminar pares
    auto nuevo_fin = std::remove_if(v.begin(), v.end(), [](int x) {
        return x % 2 == 0;
    });

    // Ejemplo 2: Borrar físicamente
    v.erase(nuevo_fin, v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 1 3 5
}
```

---

## 🧬 `std::unique`

**Descripción:** Elimina valores duplicados **consecutivos**, dejando solo una ocurrencia.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 1, 2, 2, 2, 3, 1, 1};

    // Ejemplo 1: Eliminar duplicados consecutivos
    auto nuevo_fin = std::unique(v.begin(), v.end());

    // Ejemplo 2: Borrar físicamente
    v.erase(nuevo_fin, v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 1 2 3 1
}
```
