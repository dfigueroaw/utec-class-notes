# 📘 Funciones que no modifican el rango en C++

Estas funciones de la STL **no modifican** los elementos de un contenedor. Solo los **leen** y operan sobre ellos para obtener información.

| Función     | ¿Qué hace? |
|-------------|------------|
| `for_each`  | Aplica una función a cada elemento del rango. |
| `count`     | Cuenta cuántas veces aparece un valor. |
| `any_of`    | Verifica si algún elemento cumple una condición. |
| `find`      | Busca un valor específico. |
| `mismatch`  | Encuentra la primera diferencia entre dos rangos. |

---

## 🔁 `std::for_each`

**Descripción:** Aplica una función a cada elemento del rango. No modifica a menos que la función lo haga (no recomendado si solo se quiere leer).

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v{1, 2, 3, 4, 5};

    // Ejemplo 1: Imprimir cada valor
    std::for_each(v.begin(), v.end(), [](int x) {
        std::cout << x << " ";
    });

    // Ejemplo 2: Contar los pares (solo lectura)
    int count = 0;
    std::for_each(v.begin(), v.end(), [&](int x) {
        if (x % 2 == 0) count++;
    });
    std::cout << "\nCantidad de pares: " << count;
}
````

---

## 🔢 `std::count`

**Descripción:** Cuenta cuántas veces aparece un valor dado en el rango.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 2, 3, 4, 2};

    // Ejemplo 1: Contar cuántos 2 hay
    int n = std::count(v.begin(), v.end(), 2);
    std::cout << "Cantidad de 2: " << n << "\n";

    // Ejemplo 2: Contar cuántos 5 hay
    std::cout << "Cantidad de 5: " << std::count(v.begin(), v.end(), 5) << "\n";
}
```

---

## ✅ `std::any_of`

**Descripción:** Retorna `true` si **al menos un** elemento cumple la condición.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 3, 5, 7};

    // Ejemplo 1: ¿Hay algún número par?
    bool hayPar = std::any_of(v.begin(), v.end(), [](int x) {
        return x % 2 == 0;
    });
    std::cout << "¿Hay algún par?: " << (hayPar ? "Sí" : "No") << "\n";

    // Ejemplo 2: ¿Hay algún número mayor que 6?
    std::cout << "¿Mayor que 6?: " << (std::any_of(v.begin(), v.end(), [](int x) {
        return x > 6;
    }) ? "Sí" : "No") << "\n";
}
```

---

## 🔍 `std::find`

**Descripción:** Busca un valor. Devuelve un iterador al primer hallazgo o `end()` si no lo encuentra.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{10, 20, 30, 40};

    // Ejemplo 1: Buscar 30
    auto it = std::find(v.begin(), v.end(), 30);
    if (it != v.end())
        std::cout << "Encontrado: " << *it << "\n";

    // Ejemplo 2: Buscar 50
    if (std::find(v.begin(), v.end(), 50) == v.end())
        std::cout << "50 no está en el vector\n";
}
```

---

## 🆚 `std::mismatch`

**Descripción:** Compara dos rangos y devuelve un par de iteradores donde los elementos difieren.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a{1, 2, 3, 4};
    std::vector<int> b{1, 2, 0, 4};

    // Ejemplo 1: Comparar dos vectores
    auto [it1, it2] = std::mismatch(a.begin(), a.end(), b.begin());
    if (it1 != a.end())
        std::cout << "Diferencia en: " << *it1 << " vs " << *it2 << "\n";

    // Ejemplo 2: Vectores iguales
    std::vector<int> c{1, 2, 3, 4};
    auto [it3, it4] = std::mismatch(a.begin(), a.end(), c.begin());
    if (it3 == a.end())
        std::cout << "Los vectores son iguales\n";
}
