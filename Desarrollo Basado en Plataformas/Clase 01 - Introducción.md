### Algunos protocolos para comunicarse con un API
- SOAP
- **REST** (el que se utilizará durante el curso)
- GraphQL
- gRPC

### URI, URL y Endpoint
- **URI**: Identificador genérico de un rescurso, puede ser URL o URN. **IDENTIFICA A UN RECURSO DE MANERA ÚNICA**.
- **URL**: Un tipo de URI. Tiene varias partes, por ejemplo:
	- Protocolo
	- Nombre del dominio
	- Path (Ruta)
	- File Name
- **Endpoint**: Es una **URL** específica de una API unida a un tipo de solicitud (método HTTP)

### Métodos HTTP:
- GET
- PUT
- POST
- DELETE
---
- **Seguridad**: El método HTTP no modifica el recurso en el servidor
- **Idempotencia**: Múltiples solicitudes del mismo método tienen el mismo efecto que una única solicitud.
### Códigos de Estado HTTP
Indican el resultado de una solicitud.
- **200 OK**: La solicitud fue exitosa, se devolvió el resultado esperado.
- **201 Creado**: Nuevo recurso creado exitósamente.
- **204 Sin Contenido**: Solicitud exitosa, sin contenido en la respuesta.
- **400 Solicitud Incorrecta**: La solicitud tiene parámetros inválidos o es incorrecta.
- **401 No Autorizado**: Se requiere autenticación para acceder al recurso.
- **403 Prohibido**: No tienes permiso para acceder al recurso.
- **404 No Encontrado**: El recurso solicitado no existe.
- **500 Error Interno del Servidor**: Hubo un error en el lado del servidor.
- **503 Servicio No Disponible**: El servidor está temporalmente no disponible.