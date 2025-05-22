# 🔢 Funciones de ordenación y partición en C++

Estas funciones **modifican directamente el orden del rango**, ya sea ordenándolo total o parcialmente, o dividiéndolo según un criterio lógico.

| Función         | ¿Qué hace? |
|------------------|-----------|
| `sort`           | Ordena los elementos (no estable). |
| `stable_sort`    | Ordena manteniendo el orden relativo de iguales. |
| `partition`      | Reordena colocando los que cumplen una condición al inicio. |
| `nth_element`    | Coloca el n-ésimo menor elemento en su posición final, el resto queda parcialmente ordenado. |

---

## 🔽 `std::sort`

**Descripción:** Ordena el rango usando el operador `<` o un comparador personalizado. No garantiza mantener el orden relativo de elementos iguales.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{4, 1, 3, 2};

    // Ejemplo 1: Orden ascendente
    std::sort(v.begin(), v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 1 2 3 4
}
````

---

## 🔄 `std::stable_sort`

**Descripción:** Como `sort`, pero mantiene el orden relativo de elementos con el mismo valor.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

struct Persona {
    std::string nombre;
    int edad;
};

int main() {
    std::vector<Persona> v = {
        {"Ana", 30}, {"Luis", 25}, {"Carlos", 30}
    };

    // Ejemplo 1: Ordenar por edad, mantener orden original si igual
    std::stable_sort(v.begin(), v.end(), [](const Persona& a, const Persona& b) {
        return a.edad < b.edad;
    });

    for (const auto& p : v)
        std::cout << p.nombre << " "; // Resultado: Luis Ana Carlos
}
```

---

## 📊 `std::partition`

**Descripción:** Coloca al inicio todos los elementos que cumplen con un predicado. No mantiene orden relativo.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 4, 5, 6};

    // Ejemplo 1: Mover pares al inicio
    std::partition(v.begin(), v.end(), [](int x) {
        return x % 2 == 0;
    });

    for (int x : v)
        std::cout << x << " "; // Resultado: pares al inicio, orden indefinido
}
```

---

## 🎯 `std::nth_element`

**Descripción:** Coloca el n-ésimo elemento en la posición correcta como si el rango estuviera ordenado, pero sin ordenar todo el rango.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{7, 2, 1, 5, 3, 9, 4};

    // Ejemplo 1: Colocar el 3er menor (índice 2) en su posición final
    std::nth_element(v.begin(), v.begin() + 2, v.end());

    std::cout << "3er menor elemento: " << v[2] << "\n";

    for (int x : v)
        std::cout << x << " ";
    // Resultado: El elemento en posición 2 es el correcto, los anteriores son menores (desordenados), los siguientes son mayores (desordenados)
}
```
