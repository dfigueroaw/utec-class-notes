## 1. `std::future<T>`

Un objeto que representa un **valor que estará disponible en el futuro**.
- Se usa para obtener resultados de operaciones asincrónicas.
- Se puede obtener desde `std::async`, `std::promise`, o `std::packaged_task`.

### Métodos principales

| Método         | Descripción                                                                           |
| -------------- | ------------------------------------------------------------------------------------- |
| `get()`        | Bloquea hasta que el resultado esté listo y lo retorna. Solo se puede llamar una vez. |
| `wait()`       | Bloquea hasta que el resultado esté listo. No retorna el valor.                       |
| `wait_for()`   | Espera un tiempo determinado.                                                         |
| `wait_until()` | Espera hasta una hora determinada.                                                    |
| `valid()`      | Verifica si el `future` es válido.                                                    |

---

## 2. `std::promise<T>`

Permite **producir un valor en un hilo** y que otro hilo lo reciba a través de un `std::future`.
- Tú lo completas manualmente llamando a `set_value()`.

### Métodos principales

| Método            | Descripción                     |
| ----------------- | ------------------------------- |
| `get_future()`    | Retorna el `future` asociado.   |
| `set_value(val)`  | Entrega el valor al `future`.   |
| `set_exception()` | Pasa una excepción al `future`. |
| `swap()`          | Intercambia con otra promesa.   |

---

## 3. `std::shared_future<T>`

Permite **compartir el mismo resultado** entre varios hilos. A diferencia de `std::future`, se puede copiar.
- Se obtiene llamando a `.share()` sobre un `future`.

### Métodos principales

| Método       | Descripción                                     |
| ------------ | ----------------------------------------------- |
| `get()`      | Retorna el valor (puede llamarse muchas veces). |
| `wait()`     | Espera que el valor esté listo.                 |
| `wait_for()` | Espera un tiempo limitado.                      |
| `valid()`    | Indica si aún contiene un estado válido.        |

---

## 4. `std::async`

Ejecuta una función **asincrónicamente** y retorna un `std::future` con el resultado.
- Puede usar un nuevo hilo o ejecutar en diferido según `std::launch`.

### Sintaxis

```cpp
std::async(std::launch::policy, function, args...);
```

### Políticas de lanzamiento

| Opción                  | Comportamiento                                |
| ----------------------- | --------------------------------------------- |
| `std::launch::async`    | Ejecuta en un hilo nuevo inmediatamente.      |
| `std::launch::deferred` | Ejecuta cuando llamas a `.get()` o `.wait()`. |
| (default)               | El sistema elige entre `async` o `deferred`.  |

### Métodos (heredados de `future`)

- `get()`, `wait()`, `wait_for()`, `valid()`

---

## 5. `std::packaged_task`

Es un **envoltorio para una función** que se puede ejecutar más adelante, produciendo un `std::future`.
- Útil para lanzar tareas más controladamente.
- Requiere que tú llames a `operator()` para ejecutarla.

### Sintaxis

```cpp
std::packaged_task<ReturnType(Args...)> task(callable);
```

### Métodos principales

| Método                | Descripción                            |
| --------------------- | -------------------------------------- |
| `get_future()`        | Obtiene el `future` asociado.          |
| `operator()(args...)` | Ejecuta la tarea.                      |
| `valid()`             | Indica si contiene una función válida. |
| `reset()`             | Permite reutilizarla (si está vacía).  |

---

## 🧠 Comparación general

| Herramienta          | Define tarea | Ejecuta tarea | Retorna resultado | Diferible |
| -------------------- | ------------ | ------------- | ----------------- | --------- |
| `std::future`        | ❌            | ❌             | ✅ (via .get())    | ❌         |
| `std::promise`       | ❌            | ✅ (set_value) | ✅ (via future)    | ❌         |
| `std::shared_future` | ❌            | ❌             | ✅ (muchos .get()) | ❌         |
| `std::async`         | ✅            | ✅ (auto)      | ✅ (via future)    | ✅         |
| `std::packaged_task` | ✅            | ✅ (manual)    | ✅ (via future)    | ✅         |
