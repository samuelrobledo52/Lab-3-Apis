# Reporte de API - Laboratorio 3

## 1. Información general

API utilizada: JSONPlaceholder 
Base URL: https://jsonplaceholder.typicode.com 
Tipo: REST API pública de pruebas 
Autenticación: No requiere autenticación 
Rate limit: Visible en headers (x-ratelimit-limit: 1000)

La API seleccionada es una API REST pública que permite realizar operaciones básicas sobre recursos como posts y users. Se utilizó HTTPie desde WSL para realizar todas las pruebas.

---

## 2. Variables utilizadas

Se configuraron las siguientes variables de entorno en WSL:

export BASE_URL=https://jsonplaceholder.typicode.com 
export RESOURCE=posts 
export ID=1 
export QUERY=userId==1 

Esto permitió reutilizar los comandos sin repetir la URL completa.

---

## 3. Endpoints probados

| Método | Endpoint | Parámetros | Status esperado | Status obtenido |
|--------|----------|------------|----------------|----------------|
| GET | /posts | - | 200 | 200 |
| GET | /posts/1 | - | 200 | 200 |
| GET | /posts?userId=1 | userId | 200 | 200 |
| GET | /posts?_limit=5&_page=1 | _limit, _page | 200 | 200 |
| GET | /users | - | 200 | 200 |
| POST | /posts | body JSON | 201 | 201 |
| GET | /posts/999999 | - | 404 | 404 |

---

## 4. Evidencia de respuestas exitosas

Se realizaron múltiples solicitudes exitosas:

- GET /posts → 200 OK (lista completa)
- GET /posts/1 → 200 OK (detalle por ID)
- POST /posts → 201 Created (nuevo recurso creado)

En el caso del POST, la API devolvió un nuevo ID (101) y el header Location con la URL del recurso creado.

---

## 5. Evidencia de respuestas fallidas

- GET /posts/999999 → 404 Not Found (recurso inexistente)
- Intento con parámetro inválido → 200 con lista vacía

Se observó que la API no valida estrictamente los parámetros inválidos y no implementa autenticación, por lo que no fue posible generar códigos 400, 401 o 403 reales.

---

## 6. Conclusión

Durante las pruebas se verificó el correcto funcionamiento de los endpoints principales, incluyendo lectura, filtrado, paginación y creación de recursos.

La API responde adecuadamente con códigos 200 y 201 en operaciones exitosas y 404 cuando el recurso no existe. Al ser una API educativa de pruebas, no implementa autenticación ni validaciones estrictas de entrada.

En general, la API permitió demostrar el uso correcto de HTTPie y el comportamiento básico esperado de una REST API.
