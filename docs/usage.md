# Manual de uso

Es importante identificar el valor de la variable `API_ENDPOINT` definida en el archivo __settings.py__ del proyecto. 
Esta variable se utiliza para realizar requests a los endpoints dentro del mismo proyecto. Por lo tanto, debe asegurarse
que se defina correctamente el host y el puerto.

```py
# ...

API_ENDPOINT = 'http://127.0.0.1:8011'
```
Si su proyecto corre en otro puerto deberá cambiar el valor de esta variable por el puerto correspondiente. 

Sin embargo, por default esta variable esta definida en la ip local `127.0.0.1` y en el puerto `8011` para utilizar por 
convención con el proyecto [djRefugioAnimaleCliente](https://github.com/fernandoperezwh/djRefugioAnimalesClient). 
Para más información, consulte la [documentación de djRefugioAnimaleCliente](https://github.com/fernandoperezwh/djRefugioAnimalesClient/blob/master/README.md)


## Session Authentication

Esta autentificación esta definida en el settings del proyecto. 
```py
REST_FRAMEWORK = {
    # ...
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework.authentication.SessionAuthentication', # <----
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}
```
--- 
Al iniciar el proyecto podrá visualizar en el menu del navbar que los recursos de "Personas" y "Vacunas" se encuentran
protegidos. Esto se puede ver representado por el icono de candado (cuadro rojo de la siguiente imagen) y es debido a 
que aún no se cuenta con una sesión iniciada.
![home djRefugioAnimalesTokenAuthAPI](./media/01.png)

Para acceder al recurso protegido es necesario que inicie sesión llenando los datos en el formulario de login que puede
acceder al hacer clic en el boton que se encuentra en la esquina superior derecho (flecha roja de la imagen anterior).
![Formilario inicio de sesión](./media/02.png)

Al tener iniciada su sesión ahora podrá ser capaz de acceder a los recursos que ahora se encontraran desbloqueados y que
podrá ver representados al no tener ahora el icono del candado.
![Formilario inicio de sesión](./media/03.png)


## JSON Web Token Authentication

Esta autentificación esta definida en el settings del proyecto. 
```py
REST_FRAMEWORK = {
    # ...
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework.authentication.SessionAuthentication', 
        'rest_framework_simplejwt.authentication.JWTAuthentication',  # <----
    ),
}
```
--- 
Puede interactuar con el CRUD definidos en los [endpoints de la aplicación](./endpoints.md) haciendo requests.
Para ello, en todas las peticiones debera incluir la cabecera _"Authorization"_ cuyo valor corresponde al tipo de token
y el token de acceso o access_token.
```txt
"Authorization Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwidXNlcl9pZCI6MiwianRpIjoiMDc0YmNiOTU2MzdhNGQ3NTg5ZWJkMjcxM2FiZmY3ZTEiLCJleHAiOjE2NDQ4NTU1OTZ9.8pDZRh7V_CcCusKkblKCvCNCv_SsmAuFUo0Z6Td-yio"
```

El tiempo de vida, o ttl por sus siglas en ingles _"Time To Live"_, del _"accees_token"_ esta configurado en 5 minutos.
Asi mismo, el ttl del _"refresh_token"_ esta configurado en 1 día. Siendo mas largo el tiempo para poder obtener nuevos 
_"access_token"_ mediante el _"refresh_token"_.

### Obtener access_token y refresh_token mediante la interfaz de la aplicación
Puede generar su access_token y refresh_token desde la interfaz de la aplicación siguiendo las siguientes indicaciones:
 1. Debe tener una sesión iniciada.
 2. En la vista de "home" podrá visualizar el boton _"Generar nuevo JSON Web Token"_, haga clic en el y a continuación descubrirá 
    su access_token y refresh_token.
    ![home Obtener jwt via home - button](./media/04.png)
    ![home Obtener jwt via home](./media/05.png)
 
### Obtener access_token y refresh_token mediante requests
Puede obtener su access_token y refresh_token realizando una petición `POST` al endpoint `api/auth/` pasando en el body 
un JSON que contenga su _"username"_ y _"password"_.

El siguiente cURL define lo comentado anteriormente. Puede utilizarlo como base, solo asegúrese de reemplazar los 
valores de: `<host>`, `<post>`, `<username>` y `<password>`
```bash
curl -v --location --request POST '<host>:<port>/api/auth/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "<username>",
    "password": "<password>"
}'
```


#### Ejemplo
```bash
curl -v --location --request POST 'localhost:8011/api/auth/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "fernando",
    "password": "fernando123"
}'
```
![home Obtener token via cURL](./media/06.png)

### Obtener access_token mediante el refresh_token
Si ya cuenta con un _"refresh_token"_ valido puede realizar un request a un endpoint para obtener un nuevo _"access_token"_.
Para ello se realiza una petición `POST` al endpoint `api/auth/refresh/` pasando en el body un JSON que contenga el campo
_"refresh"_ que corresponde al _"refresh_token"_.

El siguiente cURL define lo comentado anteriormente. Puede utilizarlo como base, solo asegúrese de reemplazar los 
valores de: `<host>`, `<post>` y `<refresh_token>`.
```bash
curl -v --location --request POST '<host>:<port>/api/auth/refresh/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "refresh": "<refresh_token>"
}'
```
#### Ejemplo
```bash
curl -v --location --request POST 'localhost:8011/api/auth/refresh/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsInVzZXJfaWQiOjIsImp0aSI6IjMxZmNkN2ViY2YzNDQyNDlhZjBiYjMwMjNkNDk0NDY4IiwiZXhwIjoxNjQ0OTQ0NTMzfQ.uZeZqpkfS_Q0SNoj1LTUp9wnj8o3TlpJli00er9zTCw"
}'
```
![home Obtener token via cURL](./media/07.png)

### Realizar request a un recurso protegido
Ahora que ya cuenta con su _"access_token"_ es capaz de consultar alguno de los recursos protegidos. 
A manera de ejemplo, realizaremos una consulta a la lista de personas. Sin embargo, la misma logica para la 
autentificación aplica para todos los endpoints de los modelos de la [lista de endpoints](./endpoints.md).

Para consultar la lista de personas se debe realizar una petición `GET` al endpoint `/api/persona/` y en los `headers`
debera incluir `Authorization: 'Bearer <access_token>'`.

El siguiente cURL define lo comentado anteriormente. Puede utilizarlo como base, solo asegúrese de reemplazar los 
valores de: `<host>`, `<post>`, y `<access_token>`

```bash
curl -v --location --request GET 'http://<host>:<port>/api/persona/' \
--header 'Authorization: Bearer <access_token>'
```

#### Ejemplo
```bash
curl -v --location --request GET 'http://localhost:8011/api/persona/' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwidXNlcl9pZCI6MiwianRpIjoiZDJmYjQwNzliMjU4NDlhZjllOWU3ZDYxOGRlMzZmZWMiLCJleHAiOjE2NDQ4NTcyODN9.yTIoXlQcXN7cx1jbLIkFsDmkvV480cgRZ8R8or7UPRs'
```
![home Consulta lista de personas via cURL](./media/08.png)
