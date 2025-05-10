### Ejercicio 1
```cpp
// Recorrido lineal simple  
auto count_zeros ( const std :: vector < int >& v) {  
int count = 0;  
for ( int x : v) {  
if (x == 0) ++ count ;  
}  
return count ;  
}
```
- Función de coste: $T(n)=c_1+c_2n+c_3$
- Notación asintótica: $\mathcal{O}(n)$
### Ejercicio 2
```cpp
// Suma acumulada en ventana fija  
auto window_sum ( const std :: vector < int >& v , int k) {  
std :: vector < long > sums ;  
for ( int i = 0; i + k <= ( int )v. size () ; ++ i) {  
long s = 0;  
for ( int j = 0; j < k; ++ j) s += v[i+j ];  
sums . push_back (s);  
}  
return sums ;  
}```
- Función de coste: $T(n)=c_1+(n-k+1)(c_2+c_3k+c_4)+c_5$
Desarrollando el producto, se obtiene
$$c_1+c_2n+c_3kn+c_4n-c_2k-c_3k^2-c_4k+c_2+c_3k+c_4+c_5$$
Agrupando términos
$$(c_1+c_2+c_4+c_5)+(c_3-c_2-c_4)k+(c_2+c_4)n+c_3kn-c_3k^2$$

Si $k \ll n$, podemos tomar $k$ como constante respecto a $n$.z
- Notación asintótica: $\mathcal{O}(n)$
### Ejercicio 3
```cpp
// Búsqueda de máximo local  
auto find_local_max ( const std :: vector < int >& v) {  
std :: vector < int > maxima ;  
for ( size_t i = 1; i + 1 < v. size () ; ++ i) {  
if (v[i] > v[i -1] && v[i] > v[i +1])  
maxima . push_back (v[i ]) ;  
}  
return maxima ;  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 4
```cpp
// Detección de duplicados en un vector  
# include < vector >  
# include <set >  
bool has_duplicate ( const std :: vector < int >& v) {  
std :: set < int > seen ;  
for ( int x : v) {  
// Paso 1: buscar en ’ seen ’  
if ( seen . find (x) != seen . end () )  
return true ;  
// Paso 2: insertar en ’ seen ’  
seen . insert (x);  
}  
return false ;  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 5
```cpp
// Búsqueda binaria iterativa  
int binary_search ( const std :: vector < int >& v , int x) {  
int low = 0, high = v. size () -1;  
while ( low <= high ) {  
int mid = low + ( high - low ) /2;  
if (v[ mid ] == x) return mid ;  
if (v[ mid ] < x) low = mid + 1;  
else high = mid - 1;  
}  
return -1;  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 6
```cpp
// Reducción sucesiva  
auto reduce_log ( std :: vector < int > v) {  
while (v. size () > 1) {  
v. pop_back () ;  
v. pop_back () ;  
}  
return v. front () ;  
}
```
- Función de coste: $T(n)=$
- Notación asintótica: $\mathcal{O}()$
### Ejercicio 7
```cpp
// Mezcla y ordenación de dos vectores  
# include < vector >  
# include < algorithm >  
std :: vector < int > merge_and_sort ( const std :: vector < int >& a ,  
const std :: vector < int >& b) {  
std :: vector < int > c;  
c. reserve (a. size () + b. size () ); // Paso 1  
for ( int x : a) c. push_back (x); // Paso 2  
for ( int y : b) c. push_back (y); // Paso 3  
std :: sort (c. begin () , c. end () ); // Paso 4  
return c;  
}
```
- Función de coste: $T(n)=$
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