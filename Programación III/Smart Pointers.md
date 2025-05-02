
Los **smart pointers** en C++ permiten gestionar automáticamente la memoria, reduciendo errores comunes como fugas de memoria y referencias inválidas. Se encuentran definidos en la cabecera `<memory>`.

## Unique Pointer

El `std::unique_ptr` garantiza la **propiedad exclusiva** de un objeto en memoria y se encarga de liberar automáticamente los recursos cuando el objeto deja de existir. Al no permitir que otro puntero acceda a la misma instancia, asegura una gestión eficiente y segura de la memoria, evitando posibles errores como accesos indebidos o fugas de memoria.

### Métodos principales:
- **`reset()`**: Libera el objeto gestionado.
- **`release()`**: Transfiere la propiedad sin liberar memoria.
- **`get()`**: Retorna el puntero subyacente.

### Ejemplo:

```cpp
auto ptrA = std::make_unique<Song>("El Cuarteto de Nos", "Algo mejor que hacer");
```
![[Pasted image 20250501143138.png|center]]

```cpp
auto ptrB = std::move(ptrA); // Transfiere propiedad de ptrA a ptrB
```
![[Pasted image 20250501143206.png|center]]

Cuando `ptrA` se transfiere a `ptrB`, `ptrA` queda vacío.

## Shared Pointer

El `std::shared_ptr` permite la **propiedad compartida** de un objeto en memoria mediante un **contador de referencias**, que supervisa cuántos punteros apuntan al mismo recurso. Cuando el contador llega a **cero**, la memoria se libera automáticamente, evitando fugas por referencias abandonadas. Gracias a su capacidad de gestionar múltiples accesos al mismo objeto, `std::shared_ptr` optimiza la administración de memoria sin requerir intervención manual, asegurando un control eficiente y seguro de los recursos.

### Métodos principales:
- **`reset()`**: Libera el objeto administrado.
- **`use_count()`**: Retorna cuántos `shared_ptr` están apuntando al mismo objeto.
- **`get()`**: Obtiene el puntero sin modificar el contador.

### Ejemplo:
```cpp
#include <memory>

std::shared_ptr<int> p1 = std::make_shared<int>(42);
std::shared_ptr<int> p2 = p1; // p2 ahora comparte el objeto con p1

std::cout << "Referencias activas: " << p1.use_count() << std::endl;
```

El objeto se elimina cuando **todas** las referencias desaparecen.

## Weak Pointer

El `std::weak_ptr` es un puntero observador que **no incrementa el contador de referencias** del `shared_ptr`, lo que ayuda a evitar ciclos de referencia en estructuras con enlaces mutuos. No afecta la propiedad ni la gestión de memoria, y es especialmente útil cuando se necesita una referencia a un objeto sin comprometer su ciclo de vida.
3
### Métodos principales:
- **`lock()`**: Convierte el `weak_ptr` en `shared_ptr` si el objeto aún existe.
- **`expired()`**: Verifica si el objeto ha sido eliminado.

### Ejemplo:
```cpp
#include <memory>

struct Nodo {
    std::shared_ptr<Nodo> siguiente;
    std::weak_ptr<Nodo> anterior;
};
```

Aquí, `anterior` usa `weak_ptr` para evitar un ciclo de referencia con `siguiente`.