De aquí en adelante:
- $c_n$ es una **constante arbitraria**, para todo $n \in \mathbb{N}$.
- $a_n$ refiere a una **constante amortiguada**, para todo $n \in \mathbb{N}$.
	- Cuando hay una constante amortiguada, generalmente tendrá complejidad asintótica $\mathcal{O}(1)$, sin embargo, en iteraciones específicas puede llegar a ser $\mathcal{O}(n)$. Por conveniencia, se tomará como complejidad $\mathcal{O}(1)$.
	- Por ejemplo, al insertar elementos al final de un vector, si la cantidad de elementos es menor que la capacidad, el tiempo de inserción es constante, pues el nuevo elemento se crea en un espacio libre de memoria. No obstante, cuando la cantidad de elementos alcanza la capacidad del vector, ya no se pueden realizar más inserciones de manera contigua en la memoria, por lo que es necesario copiar todos los elementos a un nuevo espacio en la memoria, lo cual escala linealmente según la cantidad de elementos. En el vector de la librería estándar, cuando se llega a este límite, el nuevo espacio reservado posee el doble de capacidad, por lo tanto, si se acaba de realizar una copia, no volverá a ocurrir hasta que la cantidad de elementos doble la actual (a menos ocurra algún tipo de intervención).

### Ejercicio 1 (ejemplo)
```cpp
auto count_zeros(const std::vector<int>& v) {
    int count = 0;
    for(int x : v) {
        if(x == 0) ++count;
    }
    return count;
}

```
- **Función de coste**: $T(n)=c_1n+c_2$
- **Notación asintótica**: $\mathcal{O}(n)$

### Ejercicio 2
```cpp
auto window_sum(const std::vector<int>& v, int k) {
    std::vector<long> sums; // Inicializar vector vacío, tiempo constante.
    for(int i = 0; i + k <= (int)v.size(); ++i) { // Recorre n - k + 1 pasos, tiempo lineal.
        long s = 0; // Inicializar variable, tiempo constante.
        for(int j = 0; j < k; ++j) // Recorre k pasos, tiempo lineal.
            s += v[i + j]; // Añadir a una variable, tiempo constante.
        sums.push_back(s); // Añadir al final de un vector, tiempo constante amortiguado.
    }
    return sums;
}
```

- **Función de coste**: $T(n, k)=c_1+(n-k+1)(c_2+c_3k+a_1)$
Dado $k \ll n$, podemos tomar $k$ como si fuera un valor constante. Finalmente se obtiene:
$$T(n)=c_1+(c_4+a_1)n$$
- **Notación asintótica**:
$$\mathcal{O}(T(n)) = \mathcal{O}(c_1+(c_4+a_1)n)$$
Usando la propiedad distributiva:
$$\mathcal{O}(T(n)) = \mathcal{O}(c_1)+\mathcal{O}((c_4+a_1)n)$$
Simplificando:
$$\mathcal{O}(T(n)) = \mathcal{O}(1) + \mathcal{O}(n)=\boxed{\mathcal{O}(n)}$$

### Ejercicio 3
```cpp
auto find_local_max(const std::vector<int>& v) {
    std::vector<int> maxima; // Inicializar vector, tiempo constante
    for(size_t i = 1; i + 1 < v.size(); ++i) { // n - 2 iteraciones, donde n es el tamaño del vector. Tiempo lineal.
        if(v[i] > v[i - 1] && v[i] > v[i + 1]) // Comparación, tiempo constante
            maxima.push_back(v[i]); // Inserción al final de un vector, complejidad amortiguada
    }
    return maxima;
}
```

- **Función de coste**: $T(n)=c+a_1(n-2)$
Desarrollando:
$$T(n)=c+a_1n-2a_1$$
Simplificando las constantes:
$$T(n)=a_1n+a_2$$
- **Notación asintótica**:
$$\mathcal{O}(T(n))=\mathcal{O}(a_1n+a_2)$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(a_1n)+\mathcal{O}(a_2)$$
Simplificando, asumiendo las constantes amortizadas como tiempo constante:
$$\mathcal{O}(T(n))=\mathcal{O}(n)+\mathcal{O}(1)=\boxed{\mathcal{O}(n)}$$

### Ejercicio 4
```cpp
#include <vector>
#include <set>

bool has_duplicate(const std::vector<int>& v) {
    std::set<int> seen; // Inicializar un set, tiempo constante
    for(int x : v) { // Iterar un vector, tiempo lineal
        if(seen.find(x) != seen.end()) // Busqueda en set, tiempo logaritmico
            return true;
        seen.insert(x); // Insertar a un set, tiempo logaritmico en relacion al tamaño del set.
    }
    return false;
} // Internamente implementa un tipo especial de Arbol de búsqueda binaria, asumiendo que es balanceado debería escalar de manera logaritmica.
```

- **Función de coste**: $T(n)=c_1+n(c_2log(n)+c_3log(n))$
Simplificando:
$$T(n)=c_1+c_4nlog(n)$$
- **Notación asintótica**:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_4nlog(n))$$
Aplicando la propiedad distributiva
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_4nlog(n))$$
Simplificando
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(nlog(n))=\boxed{\mathcal{O}(nlog(n))}$$

### Ejercicio 5
```cpp
int binary_search(const std::vector<int>& v, int x) {
    int low = 0, high = v.size() - 1; //  Asignación, tiempo constante
    while(low <= high) {
        int mid = low + (high - low)/2;
        if(v[mid] == x) return mid; // Si encuentra el resultado, lo retorna, tiempo constante
        if(v[mid] < x) low = mid + 1; // Si el target es mayor, busca en la mitad superior
        else high = mid - 1; // Si el target es menor, busca en la mitad inferior
    } // En cada busqueda (iteración) reduce el espacio a buscar por la mitad, por lo que escala logaritmicamente con respecto al tamaño del vector de entrada.
    return -1;
}
```

Sea $k$ el número de iteraciones, se puede apreciar que el tamaño del rango de búsqueda es $\frac{n}{2^k}$, el cual debería detenerse cuando tiene 1 o 0 elementos, de lo cual se obtiene la desigualdad $\frac{n}{2^k}\leq1$. Despejando, obtenemos $n\leq2^k$, y aplicando logaritmo a ambos lados se ve que $log_2(n)\leq k$, de lo cual podemos deducir que la complejidad algorítmica es logarítmica.
- **Función de coste**: $T(n)=c_1+c_2log(n)$
- **Notación asintótica**:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_2log(n))$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_2log(n))$$
Simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(log(n))=\boxed{\mathcal{O}(log(n))}$$

### Ejercicio 6
```cpp
auto reduce_log(std::vector<int> v) {
    while(v.size() > 1) {
        v.pop_back(); // Eliminar al final de un vector, tiempo constante
        v.pop_back();
    } //  Itera n/2 veces al vector
    return v.front(); // Retorna el primer elemento. Debería ocurrir un error si la cantidad de elementos es par, pues en la última iteración se eliminarían los dos últimos elementos y no habria ningún front
}
```

- **Función de coste**: $T(n)=\frac{c_1}{2}n$
- **Notación asintótica**:
$$\mathcal{O}(T(n))=\mathcal{O}(\frac{c_1}{2}n)$$
Simplificando las constantes:
$$\mathcal{O}(T(n))=\boxed{\mathcal{O}(n)}$$
### Ejercicio 7
```cpp
#include <vector>
#include <algorithm>

std::vector<int> merge_and_sort(const std::vector<int>& a, const std::vector<int>& b) {
    std::vector<int> c; // Crear nuevo vector, tiempo constante
    c.reserve(a.size() + b.size()); // Incluso si no se está moviendo memoria, la complejidad de la reserva sigue siendo lineal, aunque muy rapida pues no se está copiando data
    for(int x : a) c.push_back(x); // Insertar todos los elementos del vector a, la inserción es constante amortizada, y las la cantidad total de nservciones es lineal según la longitud del primer vector.
    for(int y : b) c.push_back(y); // Igual que en el caso anterior, lineal según la longitud del segundo vector
    std::sort(c.begin(), c.end()); // Utiliza sort de la librería estandar de C++, por lo general tiene complejidad nlogn
    return c;
}
```

- **Función de coste**: $T(n_1, n_2)=c1+c_2(n_1+n_2)+a_1n_1+a_2n_2+c_3(n_1+n_2)log(n_1+n_2)$
- **Notación asintótica**:
Primero, podemos tomar $n=\max(n_1, n_2)$ para reducir la función a una variable. No debería haber problema al realizar esta sustitución pues se está tomando el mayor tamaño entre los vectores, como si fuera una cota superior. La nueva función sería
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_2n+a_1n+c_3nlog(n))$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_2n)+\mathcal{O}(a_1n)+\mathcal{O}(c_3nlog(n))$$
Simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(n)+\mathcal{O}(n)+\mathcal{O}(nlog(n))=\boxed{\mathcal{O}(nlog(n))}$$
### Ejercicio 8
```cpp
#include <vector>
#include <algorithm>

using Interval = std::pair<int, int>;

std::vector<Interval> merge_intervals(std::vector<Interval>& intervals) {
    if(intervals.empty()) return {}; // Verificar que un vector es vacío, tiempo constante

    std::sort(intervals.begin(), intervals.end(),
              [](const Interval& a, const Interval& b) {
                  return a.first < b.first;
              }); // Ordenar un arreglo de datod, complejidad nlog(n)

    std::vector<Interval> result; // Crear un vector, tiempo constante
    result.reserve(intervals.size()); // Reservar espacio para un vector, tiempo lineal

    Interval current = intervals[0]; // Asignación, tiempo constante
    for(size_t i = 1; i < intervals.size(); ++i) { // Iterar desde el indice 1 el vector de intervalos entrada, n-1 iteraciones (lineal)
        if(intervals[i].first <= current.second) {
            current.second = std::max(current.second, intervals[i].second); // Comparación, tiempo constante
        } else {
            result.push_back(current); // Agregar elemento al vector, tiempo constante pues ya se encuentra reservado el espacio
            current = intervals[i]; // Asignación, constante
        }
    }
    result.push_back(current); // Espacio reservado, tiempo constante
    return result;
}
```

- Función de coste: $T(n)=c_1+c_2nlog(n)+c_3n+c_4(n-1)$
- Notación asintótica:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_2nlog(n)+c_3n+c_4(n-1))$$
Simplificando los terminos:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_2nlog(n)+c_5n)$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_2nlog(n))+\mathcal{O}(c_5n)$$
Simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(nlog(n))+\mathcal{O}(n)=\boxed{\mathcal{O}(nlog(n))}$$
### Ejercicio 9
```cpp
#include <vector>
#include <algorithm>

void reverse_chunks(std::vector<int>& v, int k) {
    int n = static_cast<int>(v.size()); // Typecastea el tamaño a entero, constante
    for(int i = 0; i < n; i += k) { // Iterar los elementos el vector, lineal. Itera según el tamaño del vector y el valor del step k, por lo que se podria deducir que escala segun un factor n/k.
        int left = i; // Asignación, constante
        int right = std::min(i + k - 1, n - 1); // Asignación, constante. Toma el mínimo entre el último indice del vector y el i-esimo elemento más el valor del step (k)
        while(left < right) {
            std::swap(v[left], v[right]); // Intercambiar elementos, constante
            ++left; // Aumentar valor de variable, constante
            --right; // Aumentar valor de variable, constante
        } // Itera k/2 veces, pues ambos contadores se van acercando durante cada step del while.
    }
}
```

- Función de coste: $T(n, k)=c_1+\left\lceil \frac{n}{k} \right\rceil(c_2+c_3\left\lfloor \frac{k}{2} \right\rfloor)$
- Notación asintótica: Sabiendo que $k$ es menor que $n$, podemos tomarla como una entrada de orden constante respecto a n. La función de costo entonces tendría la forma:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_4n)$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_4n)$$
Finalmente, simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(n)=\boxed{\mathcal{O}(n)}$$
### Ejercicio 10
```cpp
#include <vector>

void rotate_right(std::vector<int>& v, int k) {
    int n = v.size(); // Asignación, tiempo constante
    k = k % n; // Operador modulo, tiempo constante
    std::vector<int> tail(v.end() - k, v.end()); // Copia los k ultimos elementos del vector, complejidad lineal respecto a k
    for(int i = n - 1; i >= k; --i) // Itera desde el ultimo elemento hasta el k-esimo elemento (n-k iteraciones)
        v[i] = v[i - k]; // Asignación, constante
    for(int i = 0; i < k; ++i) // Itera desde el primer elemento hasta el anterior al k-esimo elemento, lineal (k iteraciones)
        v[i] = tail[i];// Asignación, constante
} // Entre los dos últimos bucles, ocurren n - k + k = n iteraciones
```

- Función de coste: $T(n, k)=c_1+c_2k+c_3n$
- Notación asintótica: Sabemos que $k<n$, por lo que podemos tomar la complejidad respecto a $n$ y a $k$ como constante.
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_2k+c_3n)$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_2k)+\mathcal{O}(c_3n)$$
Simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(1)+\mathcal{O}(1)+\mathcal{O}(n)=\boxed{\mathcal{O}(n)}$$
