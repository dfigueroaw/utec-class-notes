## 1. `std::mutex`

**Descripción:**  
Un mutex (mutual exclusion) es un objeto que garantiza acceso exclusivo a una sección crítica de código. Solo un hilo puede poseer el mutex a la vez. Cuando un hilo adquiere el mutex, otros hilos que intenten adquirirlo quedan bloqueados hasta que se libere.

**Características:**
- Permite proteger secciones críticas para evitar condiciones de carrera.
- Bloquea el hilo que intenta adquirir el mutex si está ocupado.
- Debe ser desbloqueado explícitamente para liberar la exclusión.

**Métodos principales:**
- `lock()` — bloquea el mutex, espera si está bloqueado.
- `unlock()` — desbloquea el mutex, permitiendo que otro hilo lo adquiera.
- `try_lock()` — intenta bloquear el mutex sin bloqueo; retorna `true` si tuvo éxito o `false` si está bloqueado.

---

## 2. `std::lock_guard<std::mutex>`

**Descripción:**  
Es una clase RAII que bloquea automáticamente un mutex al crearse y lo desbloquea al destruirse. Simplifica la gestión de mutex evitando olvidos al desbloquear, especialmente ante excepciones.

**Características:**
- Bloquea el mutex en el constructor.
- Desbloquea el mutex automáticamente en el destructor (al salir del scope).
- No permite desbloqueo manual ni reapertura del mutex.

**Métodos principales:**
- Constructor `lock_guard(mutex&)` — bloquea el mutex.
- Destructor — desbloquea automáticamente el mutex.

---

## 3. `std::unique_lock<std::mutex>`

**Descripción:**  
Clase RAII más flexible que `lock_guard`. Permite bloquear y desbloquear el mutex manualmente dentro de un scope. También puede diferir el bloqueo o transferir la propiedad del mutex.

**Características:**
- Permite bloquear y desbloquear manualmente.
- Permite diferir bloqueo al crear la instancia (`defer_lock`).
- Permite transferir la propiedad del mutex entre `unique_lock`s.

**Métodos principales:**

- `lock()` — bloquea el mutex (si no está bloqueado).
- `unlock()` — desbloquea el mutex (si está bloqueado).
- `try_lock()` — intenta bloquear sin esperar, devuelve bool.
- `owns_lock()` — indica si posee el mutex actualmente.
- `release()` — libera la propiedad del mutex sin desbloquearlo (devuelve puntero al mutex).
- Constructor con opciones: bloqueo inmediato, diferido, etc.

---

## 4. `std::atomic<T>`

**Descripción:**  
Tipo de dato atómico que permite operaciones atómicas indivisibles en variables básicas (int, bool, punteros, etc.), sin necesidad de mutex. Previene condiciones de carrera en operaciones simples.

**Características:**
- Operaciones atómicas y lock-free (si el hardware lo soporta).
- Permite lectura, escritura y operaciones aritméticas atómicas.
- Soporta operaciones avanzadas como compare-and-swap.

**Métodos principales:**
- `load()` — obtiene el valor atómicamente.
- `store()` — almacena un valor atómicamente.
- `fetch_add()`, `fetch_sub()`, `fetch_and()`, `fetch_or()`, `fetch_xor()` — operaciones aritméticas atómicas que retornan el valor previo.
- `compare_exchange_strong(expected, desired)` — compara el valor actual con `expected`; si coinciden, asigna `desired`.
- `compare_exchange_weak(expected, desired)` — igual que `strong` pero puede fallar espuriamente, útil en bucles.

---

## 5. `std::atomic_flag`

**Descripción:**  
El tipo atómico más simple, representa un flag booleano atómico que solo admite dos operaciones: test-and-set y clear. Es útil para implementar spinlocks o banderas muy ligeras.

**Características:**
- Solo dos estados: `set` (true) y `clear` (false).
- Operaciones atómicas muy rápidas.
- No puede ser copiado ni asignado.

**Métodos principales:**
- `test_and_set(memory_order)` — pone el flag a `true` y devuelve el valor previo.
- `clear(memory_order)` — pone el flag a `false`.

---

## 6. `std::binary_semaphore`

**Descripción:**  
Semáforo que solo admite dos estados: 0 o 1. Controla el acceso a un recurso único o la sincronización entre hilos que necesitan señalizar y esperar eventos.

**Características:**
- Internamente mantiene un contador binario (0 o 1).
- Operaciones de espera bloqueante y no bloqueante.
- Puede ser usado para señalizar entre hilos.

**Métodos principales:**
- `acquire()` — espera hasta que el semáforo esté disponible (valor 1) y lo toma (decrementa a 0). Bloqueante.
- `try_acquire()` — intenta adquirir sin bloquear, devuelve `true` si tuvo éxito.
- `release()` — libera el semáforo (incrementa el contador a 1).
- `try_acquire_for(duration)` / `try_acquire_until(time_point)` — espera con timeout.

---

## 7. `std::counting_semaphore<Max>`

**Descripción:**  
Semáforo con contador que puede tener valores de 0 hasta un máximo `Max`. Controla acceso concurrente a un número limitado de recursos iguales.

**Características:**
- Permite que hasta `Max` hilos tengan acceso simultáneo.
- Muy útil para limitar concurrencia o manejar pools de recursos.

**Métodos principales:**
- `acquire()` — espera y decrece el contador. Bloqueante si contador es 0.
- `try_acquire()` — intenta adquirir sin bloqueo.
- `release()` — incrementa el contador, liberando recursos.
- Igual que `binary_semaphore` pero con contador variable.
