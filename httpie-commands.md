httpie-commands.md
# HTTPie Commands - Lab 3 APIs

## Variables de entorno utilizadas

bash
export BASE_URL=https://jsonplaceholder.typicode.com
export RESOURCE=posts
export ID=1
export QUERY=userId==1
1. Listar recurso principal
http GET $BASE_URL/$RESOURCE
2. Obtener detalle por ID
http GET $BASE_URL/$RESOURCE/$ID
3. Búsqueda por query parameter
http GET $BASE_URL/$RESOURCE $QUERY
4. Filtro avanzado (múltiples parámetros)
http GET $BASE_URL/$RESOURCE userId==1 id==1
5. Paginación
http GET $BASE_URL/$RESOURCE _limit==5 _page==1
6. Segundo recurso
http GET $BASE_URL/users
7. Solicitud real (POST)
http POST $BASE_URL/posts \
title="Lab 3" \
body="Prueba real desde WSL" \
userId:=1
8. Recurso inexistente (404)
http GET $BASE_URL/posts/999999
9. Header personalizado
http GET $BASE_URL/$RESOURCE Accept:application/json
10. Intento con parámetro inválido
http GET "$BASE_URL/$RESOURCE?id=abc"

Nota: la API devuelve 200 con lista vacía ya que no valida estrictamente los parámetros.
