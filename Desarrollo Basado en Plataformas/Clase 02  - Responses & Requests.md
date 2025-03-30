## Información adicional - Request

### Query Parameter
Añade **información adicional** para modificar o afinar la solicitud **sin cambiar la identificación principal** del recurso. Generalmente...
- Se envían como parte del URL después del símbolo **?**.
- Se representan en pares **clave-valor**, separados por el símbolo **&**.
### Path Parameter
Identifica un recurso específico en el servidor. Se envían como parte de la ruta o endpoint de la URL y suelen ser obligatorios.
### Request Body
Datos adicionales para crear, actualizar o realizar operaciones complejas sobre el recurso específico. Especialmente útil cuando hay necesidad de enviar información estructurada, como un objeto completo. Para esto, podemos apoyarnos, por ejemplo, del uso de **Pydantic**.
## Características - Response

### Status Code
Indica el **estado general de la respuesta**, incluido el código de estado y el mensaje de estado.
### Headers
Información adicional sobre la respuesta o el servidor, como el tipo y longitud del contenido y directivas de almacenamiento en caché.
### Body
Contiene los datos solicitados por el servidor, a menudo en formatos como **JSON**, **XML** o textos sin formato.

## Ejemplo con FastAPI
```python

```

