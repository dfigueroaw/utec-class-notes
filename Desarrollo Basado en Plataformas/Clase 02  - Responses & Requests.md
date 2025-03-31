## Información adicional - Request

### Query Parameter
Añade **información adicional** para modificar o afinar la solicitud **sin cambiar la identificación principal** del recurso. Generalmente...
- Se envían como parte del URL después del símbolo **?**.
- Se representan en pares **clave-valor**, separados por el símbolo **&**.
### Path Parameter
Identifica un recurso específico en el servidor. Se envían como parte de la ruta o endpoint de la URL y suelen ser obligatorios.
### Request Body
Datos adicionales para crear, actualizar o realizar operaciones complejas sobre el recurso específico. Especialmente útil cuando hay necesidad de enviar información estructurada, como un objeto completo. Para esto, podemos apoyarnos, por ejemplo, del uso de **Pydantic**.
#### Ejemplo
```python
PUT /api/users/123?include=details HTTP/1.1
Host: api.example.com
Content-Type: application/json
Content-Length: 85
Authorization: Bearer abcdef123456
Accept: */*

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "status": "active"
}
```

## Características - Response

### Status Code
Indica el **estado general de la respuesta**, incluido el código de estado y el mensaje de estado.
### Headers
Información adicional sobre la respuesta o el servidor, como el tipo y longitud del contenido y directivas de almacenamiento en caché.
### Body
Contiene los datos solicitados por el servidor, a menudo en formatos como **JSON**, **XML** o textos sin formato.
#### Ejemplo
```python
# Status Code
HTTP/1.1 200 OK
# Header
Content-Type: application/json
Content-Length: 85
Date: Wed, 24 Jul 2024 12:28:53 GMT
Server: Apache/2.4.41 (Ubuntu)

# Body
{
  "id": 123,
  "name": "John Doe",
  "email": "john.doe@example.com",
  "status": "active"
}
```

## Ejemplo con FastAPI
### anime.py
```python
from pydantic import BaseModel  
from typing import List  
  
class Anime(BaseModel):  
    title: str  
    season: str  
    kind: str  
    coverImageUrl: str  
    rating: int  
    reviews: int  
    genres: List[str]
```
### main.py
```python
from fastapi import FastAPI  
from anime import Anime  
app = FastAPI()  
  
# Los Pokemon son imágenes temporales, esto es únicamente un ejemplo  
animes = [  
{  
    "coverImageUrl": "https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/001.png",  
    "title": "Gintama: THE FINAL",  
    "genres": ["action", "comedy", "drama", "sci-fi"],  
    "rating": 91,  
    "kind": "Movie",  
    "reviews": 38620,  
    "season": "Winter 2021"  
},  
{  
    "coverImageUrl": "https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/004.png",  
    "title": "Fruits Basket: The Final",  
    "genres": ["comedy", "drama", "psychological"],  
    "rating": 90,  
    "kind": "TV Show",  
    "reviews": 37891,  
    "season": "Spring 2021"  
},  
{  
    "coverImageUrl": "https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/007.png",  
    "title": "Hagane no Renkinjutsushi: FULLMETAL ALCHEMIST",  
    "genres": ["action", "adventure", "drama", "fantasy"],  
    "rating": 89,  
    "kind": "TV Show",  
    "reviews": 34600,  
    "season": "Spring 2009"  
},  
{  
    "coverImageUrl": "https://www.pokemon.com/static-assets/content-assets/cms2/img/pokedex/full/010.png",  
    "title": "One Piece",  
    "genres": ["adventure", "action", "drama", "fantasy"],  
    "rating": 100,  
    "kind": "TV Show",  
    "reviews": 100000,  
    "season": "Spring 2024"  
}  
]  
  
@app.get('/')  
def home():  
    return "Welcome to Anime API! [TEST]"  
  
@app.get('/animes')  
def list_animes():  
    return animes  
  
@app.post('/animes')  
def create_anime(anime: Anime):  
    animes.append(anime)  
    return anime  
  
@app.get('/animes/{index}')  
def read_anime(index: int):  
    return animes[index]  
  
@app.put('/animes/{index}')  
def update_anime(index: int, anime: Anime):  
    animes[index] = anime  
    return anime  
  
@app.delete('/animes/{index}')  
def delete_anime(index: int):  
    deleted = animes[index]  
    animes.pop(index)  
    return deleted
```
