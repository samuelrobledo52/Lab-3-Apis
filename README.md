# Lab-3-Apis

## 1. Resumen de la API

**Nombre:** JSONPlaceholder  
**Base URL:** https://jsonplaceholder.typicode.com  
**Tipo:** REST API pública de pruebas  
**Autenticación:** No requiere autenticación  
**Rate Limit:** Visible en headers (x-ratelimit-limit: 1000)

La API seleccionada es JSONPlaceholder, una API REST pública utilizada comúnmente para pruebas y aprendizaje. Permite realizar operaciones CRUD sobre recursos como posts, users y comments. No requiere autenticación y responde en formato JSON.



## 2. Variables utilizadas (WSL)

En WSL se configuraron variables de entorno para facilitar las pruebas:


export BASE_URL=https://jsonplaceholder.typicode.com
export RESOURCE=posts
export ID=1
export QUERY=userId==1
<img width="1036" height="103" alt="Variables Configuradas" src="https://github.com/user-attachments/assets/238dddf1-e107-4304-a4ce-0e9f553c5e25" />



3. Happy Path (Pruebas exitosas)
3.1 Listar recurso principal
http GET $BASE_URL/$RESOURCE

Status obtenido: 200 OK
La API devuelve los 100 posts disponibles.

<img width="1472" height="668" alt="Resource" src="https://github.com/user-attachments/assets/39a15fc5-c656-4a93-bd45-71fa7cd0f253" />


3.2 Detalle por ID
http GET $BASE_URL/$RESOURCE/$ID

Status obtenido: 200 OK
Se obtiene únicamente el post con id=1.
<img width="1462" height="547" alt="Id" src="https://github.com/user-attachments/assets/04e21707-be9f-452c-9da2-62dfb91be23c" />



3.3 Búsqueda por query param
http GET $BASE_URL/$RESOURCE $QUERY

Status obtenido: 200 OK
Se filtran los posts correspondientes al userId=1.
<img width="1466" height="627" alt="Query " src="https://github.com/user-attachments/assets/83c492a3-e71b-4be5-b032-220eb936bd51" />


3.4 Filtro avanzado
http GET $BASE_URL/$RESOURCE userId==1 id==1

Status obtenido: 200 OK
Se combinan dos parámetros y retorna un solo registro.
<img width="1452" height="557" alt="Filtro avanzado" src="https://github.com/user-attachments/assets/14747b6c-a14c-4a6c-ad28-e9e750b5f46b" />

3.5 Paginación
http GET $BASE_URL/$RESOURCE _limit==5 _page==1

Status obtenido: 200 OK
Se devuelven únicamente 5 registros.
En los headers se observa:

x-total-count: 100

link: first, next, last

Esto confirma que la API soporta paginación.
<img width="1477" height="677" alt="Paginacion " src="https://github.com/user-attachments/assets/3258ef12-0c60-436f-a757-53bd8b1dcd52" />


3.6 Segundo recurso
http GET $BASE_URL/users

Status obtenido: 200 OK
Se obtiene la lista completa de usuarios.
<img width="1455" height="647" alt="Segundo recurso" src="https://github.com/user-attachments/assets/3a74018a-df8a-4819-b6fa-1d6025322f06" />


4. Solicitud real (POST)

Se realizó una solicitud para crear un nuevo recurso:

http POST $BASE_URL/posts \
title="Lab 3" \
body="Prueba real desde WSL" \
userId:=1

Status obtenido: 201 Created

La respuesta incluye:

Nuevo ID generado (101)

Header Location con la URL del recurso creado

Esto confirma que la API permite creación de recursos correctamente.
<img width="1453" height="628" alt="Prueba real" src="https://github.com/user-attachments/assets/3f5b1b9f-a7fd-434b-9631-a00f562822f2" />


5. Pruebas de error
5.1 Recurso inexistente (404)
http GET $BASE_URL/posts/999999

Status obtenido: 404 Not Found

La API responde correctamente cuando el recurso no existe.
<img width="1461" height="527" alt="Not found" src="https://github.com/user-attachments/assets/67b5886a-2a70-47cd-8eda-c82fd13cc9cf" />

5.2 Intento de generar 400, 401 y 403

Se intentaron generar errores adicionales enviando parámetros inválidos y headers de autenticación incorrectos. Sin embargo:

La API no implementa autenticación.

No valida estrictamente parámetros inválidos.

En algunos casos devuelve 200 con lista vacía en lugar de 400.

Esto se debe a que JSONPlaceholder es una API de pruebas y no implementa validaciones completas como una API productiva.
<img width="1462" height="631" alt="Otro error" src="https://github.com/user-attachments/assets/070e560f-57ff-4ff2-bad5-9adb9ec5a3c8" />


6. Conclusión

Durante las pruebas se pudo verificar el correcto funcionamiento de los endpoints principales, incluyendo lectura, filtrado, paginación y creación de recursos. La API responde adecuadamente con códigos 200 y 201 en operaciones exitosas y 404 en recursos inexistentes.

También se observó que al ser una API educativa no implementa autenticación ni validaciones estrictas, lo cual explica la ausencia de códigos 400, 401 o 403 reales.

En general, la API cumple con el comportamiento esperado de una REST API básica y permitió demostrar el uso correcto de HTTPie desde WSL.
