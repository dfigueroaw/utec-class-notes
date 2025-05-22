# 📦 Funciones que copian o mueven rangos en C++

Estas funciones **generan un rango de destino**, copiando o moviendo elementos desde el rango de origen. El rango de origen **queda igual** (excepto en el caso de `move`, donde los objetos fuente quedan en estado válido pero no definido).

| Función         | ¿Qué hace? |
|------------------|-----------|
| `copy`           | Copia todos los elementos del rango. |
| `copy_if`        | Copia solo los que cumplen una condición. |
| `move`           | Mueve los elementos (transfiere recursos). |
| `swap_ranges`    | Intercambia elementos de dos rangos. |
| `transform`      | Aplica una función y copia el resultado a un nuevo rango. |

---

## 📄 `std::copy`

**Descripción:** Copia todos los elementos de un rango a otro.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> origen{1, 2, 3, 4};
    std::vector<int> destino(origen.size());

    // Ejemplo 1: Copiar todos los elementos
    std::copy(origen.begin(), origen.end(), destino.begin());

    for (int x : destino)
        std::cout << x << " ";
}
````

---

## 🎯 `std::copy_if`

**Descripción:** Copia solo los elementos que cumplen una condición.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> origen{1, 2, 3, 4, 5, 6};
    std::vector<int> destino;

    // Ejemplo 1: Copiar solo pares
    std::copy_if(origen.begin(), origen.end(), std::back_inserter(destino), [](int x) {
        return x % 2 == 0;
    });

    for (int x : destino)
        std::cout << x << " ";
}
```

---

## 🚚 `std::move`

**Descripción:** Mueve elementos (transfiere recursos al destino).

```cpp
#include <vector>
#include <algorithm>
#include <iostream>
#include <string>

int main() {
    std::vector<std::string> origen{"uno", "dos", "tres"};
    std::vector<std::string> destino(origen.size());

    // Ejemplo 1: Mover strings
    std::move(origen.begin(), origen.end(), destino.begin());

    std::cout << "Destino:\n";
    for (const auto& s : destino) std::cout << s << " ";

    std::cout << "\nOrigen después del move:\n";
    for (const auto& s : origen) std::cout << "[" << s << "] ";
}
```

---

## 🔄 `std::swap_ranges`

**Descripción:** Intercambia elementos entre dos rangos del mismo tamaño.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a{1, 2, 3};
    std::vector<int> b{4, 5, 6};

    // Ejemplo 1: Intercambiar elementos
    std::swap_ranges(a.begin(), a.end(), b.begin());

    std::cout << "a: ";
    for (int x : a) std::cout << x << " ";

    std::cout << "\nb: ";
    for (int x : b) std::cout << x << " ";
}
```

---

## 🔧 `std::transform`

**Descripción:** Aplica una función a cada elemento del rango y guarda el resultado en otro.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> origen{1, 2, 3, 4};
    std::vector<int> destino(origen.size());

    // Ejemplo 1: Multiplicar por 10
    std::transform(origen.begin(), origen.end(), destino.begin(), [](int x) {
        return x * 10;
    });

    for (int x : destino)
        std::cout << x << " ";
}
```
