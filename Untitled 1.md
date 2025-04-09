Un usuario **no necesariamente** es un cliente. Más que nada porque el usuario usualmente interactúa con alguna capa de abstracción para realizar un *request* al servidor.

Esencialmente, el usuario desea hacer algo, implementa lo que quiere hacer en el *client*, el *client* lanza un *request* al servidor, el *server* busca o reemplaza algo en el *database*. Luego, en sentido inverso, se envía la información buscada de vuelta al *client*, para que el usuario pueda observar que la acción fue realizada.

### :LiBookOpen: *Error handling*

***Error handling*** es informar al usuario, al igual que si todo esté bien, sobre **un error que haya ocurrido en alguna capa de la aplicación**. Es nuestro deber como desarrolladores aprender a manejar esta información.

Hemos aclarado que íbamos a seguir una estructura para la arquitectura del backend: dominio (entidad y repositorio), servicio y controlador. Por ejemplo, en la entidad `calculadora`, el repositorio sería `calculatorRepository`, su servicio `calculatorService`, y así.

Digamos que queremos implementar la división dentro de esta calculadora.

```
@RestController
@RequestMapping("/calculator)
public class CalculatorController {
	@Autowired
	private CalculatorService service;
	@GetMapping("/divide/{a}/{b}/)
	public Double divide(@PathVariable Long a, @PathVariable Long b) {
		return service.divide(a,b);
	}
}
```

Este sería el server:

```
@Service
@Transactional
publoc class CalculatorService {
	@Autowired
	private CalculatorRepository repository;
	public Double divide(Long a, Long b) {
		return a/b;
	}
}
```

Esto depende de lo que ingrese el usuario en el URL. Pero, ¿qué pasa si `b=0`? ¿O si algún parámetro es un carácter en vez de un número?

Para esto, podemos crear un sistema ***try/catch***. Podemos interpretar *try* como un "si ocurre un error", y el *catch* como un "hacer esto si ocurre un error".

Si implementamos esto en nuestro caso específico, podemos implementar el siguiente código  dentro de la función `divide(...)`:

```
if (a == null || b == null) {
	throw new IllegalArgumentException("'a' y 'b' no pueden ser nulos.");
}
if (b == 0) {
	throw new ArithmeticException("División por cero no permitida.");
}
return a/b;
```

Esto es **propagar el error**: encontrar y solucionar los errores. **Es ideal nunca asumir que algo es intuitivo porque el usuario es capaz de cualquier cosa, y es capaz de encontrar todos estos errores accidentalmente**.

Nota: `IllegalArgumentException(...) y ArithmeticException(...)` son **esencialmente alertas**. Podemos crearlas nosotros a nuestro gusto: `public class MatiasException { ...; }`, siempre y cuando extienda a `Exception`.

**Manejar** el error es implementar el try/catch dentro del controlador:

```
try {
	Double result = service.divide(a, b);
	return ResponseEntity.ok(result);
} catch (IllegalArgumentException e) {
	return ResponseEntity.status(HttpStatus.UNPROCESSABLE_ENTITY).body("Error aritmético: " + e.getMessage());
} catch (ArithmeticException e) {
	return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Error interno inesperado: " + e.getMessage());
}
```

### :LiBookOpen: Más cosas del status code

El primer dígito del status code ayuda a intuir qué ocurrió.
1. informativo
2. éxito. No hay ningún problema, el servidor entiende y procesa la petición y se retorna lo que se desea.
3. redirección. El servidor al que se solicita no tiene la información requerida, pero conoce de otro recurso que **sí** tiene el recurso buscado. Esto es usualmente automático y se redirige.
4. error del cliente. El *client* no puede procesar ni realizar la consulta brindada por el usuario.
5. error del servidor. Hay cierto problema dentro del *server* que no se puede resolver a simple vista.