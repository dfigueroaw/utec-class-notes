# 🔧 Funciones de mutación estructural en C++

Estas funciones **modifican el contenido o el orden del rango** directamente (in-place). A diferencia de `copy` o `remove`, **sí alteran** el contenedor original.

| Función     | ¿Qué hace? |
|-------------|------------|
| `reverse`   | Invierte el orden de los elementos. |
| `rotate`    | Rota los elementos (pone otro inicio). |
| `fill`      | Rellena todos los elementos con un valor. |
| `generate`  | Rellena con los valores devueltos por una función. |
| `shuffle`   | Mezcla aleatoriamente los elementos. |

---

## 🔁 `std::reverse`

**Descripción:** Invierte el orden de los elementos en el rango.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 4};

    // Ejemplo 1: Invertir in-place
    std::reverse(v.begin(), v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 4 3 2 1
}
````

---

## 🔄 `std::rotate`

**Descripción:** Rota los elementos para que uno en medio sea el nuevo inicio.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 4, 5};

    // Ejemplo 1: Rotar para que el elemento en la posición 2 (índice) sea el nuevo inicio
    std::rotate(v.begin(), v.begin() + 2, v.end());

    for (int x : v)
        std::cout << x << " "; // Resultado: 3 4 5 1 2
}
```

---

## 🧪 `std::fill`

**Descripción:** Rellena todo el rango con un mismo valor.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v(5);

    // Ejemplo 1: Llenar con el valor 7
    std::fill(v.begin(), v.end(), 7);

    for (int x : v)
        std::cout << x << " "; // Resultado: 7 7 7 7 7
}
```

---

## ⚙️ `std::generate`

**Descripción:** Rellena el rango con valores producidos por una función.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v(5);
    int contador = 1;

    // Ejemplo 1: Llenar con números consecutivos desde 1
    std::generate(v.begin(), v.end(), [&]() {
        return contador++;
    });

    for (int x : v)
        std::cout << x << " "; // Resultado: 1 2 3 4 5
}
```

---

## 🎲 `std::shuffle`

**Descripción:** Mezcla aleatoriamente los elementos usando un generador de números aleatorios.

```cpp
#include <vector>
#include <algorithm>
#include <random>
#include <iostream>

int main() {
    std::vector<int> v{1, 2, 3, 4, 5};

    // Ejemplo 1: Mezclar aleatoriamente usando random device
    std::random_device rd;
    std::mt19937 g(rd());

    std::shuffle(v.begin(), v.end(), g);

    for (int x : v)
        std::cout << x << " "; // Resultado: orden aleatorio
}
```
