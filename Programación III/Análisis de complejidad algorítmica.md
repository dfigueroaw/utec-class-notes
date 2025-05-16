De aquí en adelante:
- $c_n$ es una **constante arbitraria**, para todo $n \in \mathbb{N}$.
- $a_n$ refiere a una **constante amortiguada**, para todo $n \in \mathbb{N}$.
	- Cuando hay una constante amortiguada, generalmente tendrá complejidad asintótica $\mathcal{O}(1)$, sin embargo, en iteraciones específicas puede llegar a ser $\mathcal{O}(n)$. Por conveniencia, se tomará como complejidad $\mathcal{O}(1)$.
	- Por ejemplo, al insertar elementos al final de un vector, si la cantidad de elementos es menor que la capacidad, el tiempo de inserción es constante, pues el nuevo elemento se crea en un espacio libre de memoria. No obstante, cuando la cantidad de elementos alcanza la capacidad del vector, ya no se pueden realizar más inserciones de manera contigua en la memoria, por lo que es necesario copiar todos los elementos a un nuevo espacio en la memoria, lo cual escala linealmente según la cantidad de elementos. En el vector de la librería estándar, cuando se llega a este límite, el nuevo espacio reservado posee el doble de capacidad, por lo tanto, si se acaba de realizar una copia, no volverá a ocurrir hasta que la cantidad de elementos doble la actual (a menos ocurra algún tipo de intervención).
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
}```
- Función de coste: $T(n, k)=c_1+(n-k+1)(c_2+c_3k+a_1)$
Dado $k \ll n$, podemos tomar $k$ como si fuera un valor constante. Finalmente se obtiene:
$$T(n)=a+bn$$
- Notación asintótica:
$$\mathcal{O}(T(n)) = \mathcal{O}(a+bn)$$
Usando la propiedad distributiva:
$$\mathcal{O}(T(n)) = \mathcal{O}(a)+\mathcal{O}(bn)$$
Simplificando:
$$\mathcal{O}(T(n)) = \mathcal{O}(n)$$
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
- Función de coste: $T(n)=c+a_1(n-2)$
Desarrollando:
$$T(n)=c+a_1n-2a_1$$
Simplificando las constantes:
$$T(n)=a_1n+a_2$$
- Notación asintótica:
$$\mathcal{O}(T(n))=\mathcal{O}(a_1n+a_2)$$
Aplicando la propiedad distributiva:
$$\mathcal{O}(T(n))=\mathcal{O}(a_1n)+\mathcal{O}(a_2)$$
Simplificando, asumiendo las constantes amortizadas como tiempo constante:
$$\mathcal{O}(T(n))=\mathcal{O}(n)$$

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
- Función de coste: $T(n)=c_1+n(c_2log(n)+c_3log(n))$
Simplificando:
$$T(n)=c_1+c_4nlog(n)$$
- Notación asintótica:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1+c_4nlog(n))$$
Aplicando la propiedad distributiva
$$\mathcal{O}(T(n))=\mathcal{O}(c_1)+\mathcal{O}(c_4nlog(n))$$
Simplificando
$$\mathcal{O}(T(n))=\mathcal{O}(nlog(n))$$
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
- Función de coste: $T(n)=c_1log(n)$
- Notación asintótica:
$$\mathcal{O}(T(n))=\mathcal{O}(c_1log(n))$$
Simplificando:
$$\mathcal{O}(T(n))=\mathcal{O}(log(n))$$
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
- Función de coste: $T(n)=\frac{c_1}{2}n$
- Notación asintótica:
$$\mathcal{O}(T(n))=\mathcal{O}(\frac{c_1}{2}n)$$
Simplificando las constantes:
$$\mathcal{O}(T(n))=\mathcal{O}(n)$$
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
- Función de coste: $T(n_1, n_2)=c1+c_2(n_1+n_2)+c_3n_1+c_4n_2$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 8
```cpp
# include < vector >  
# include < algorithm >  
using Interval = std :: pair < int , int >;  
std :: vector < Interval > merge_intervals ( std :: vector < Interval >& intervals ) {  
if ( intervals . empty () )  
return {};  
// Paso 1: ordenar por el inicio de cada intervalo  
std :: sort ( intervals . begin () , intervals . end () ,  
[]( const Interval & a , const Interval & b){  
return a. first < b. first ;  
}) ; // C1 : comparaci ón  
std :: vector < Interval > result ;  
result . reserve ( intervals . size () ); // C2 : reserva  
// Paso 2: inicializar el intervalo actual  
Interval current = intervals [0]; // C3 : asignaci ón  
// Paso 3: recorrer y fusionar  
for ( size_t i = 1; i < intervals . size () ; ++ i) { // C4 : bucle  
if ( intervals [i ]. first <= current . second ) {  
// solapan : ampliamos el extremo derecho  
current . second = // C5 : comparaci ón + asignaci ón  
std :: max ( current . second , intervals [i ]. second );  
} else {  
// no solapan : guardamos el actual y pasamos al siguiente  
result . push_back ( current ); // C6 : push_back  
current = intervals [i ]; // C7 : asignaci ón  
}  
}  
// Paso 4: añ adir el ú ltimo  
result . push_back ( current ); // C8 : push_back  
return result ; // C9 : return  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 9
```cpp
// revierte cada bloque ( chunk ) de tamaño k en el vector  
# include < vector >  
# include < algorithm >  
void reverse_chunks ( std :: vector < int >& v , int k) {  
int n = static_cast < int >( v. size () ); // C1 : lectura de tama ño  
for ( int i = 0; i < n; i += k) { // C2 : bucle externo  
// ~ n/k iteraciones  
int left = i;  
int right = std :: min (i + k - 1, n - 1) ;  
while ( left < right ) { // C3 : cada swap  
// ~ suma de chunk /2 iteraciones  
std :: swap (v[ left ], v[ right ]) ;  
++ left ; // C4 : incremento de í ndice  
-- right ; // C4 : decremento de í ndice  
}  
}  
// C5 : costes fijos ( control de bucles , return , etc .)  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 10
```cpp
// Rotación de elementos en un vector  
# include < vector >  
void rotate_right ( std :: vector < int >& v , int k) {  
int n = v. size () ;  
// Paso 1: ajustar k si es mayor que n  
k = k % n;  
// Paso 2: guardar los ú ltimos k en auxiliar  
std :: vector < int > tail (v. end () -k , v. end () );  
// Paso 3: desplazar los primeros n -k posiciones  
for ( int i = n -1; i >= k; --i)  
v[i] = v[i -k ];  
// Paso 4: colocar el auxiliar al inicio  
for ( int i = 0; i < k; ++ i)  
v[i] = tail [i ];  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$