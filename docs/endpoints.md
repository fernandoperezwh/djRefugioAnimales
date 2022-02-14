# Lista de endpoints

## Autentificación
- POST api/auth/ -- Obtiene el _"access_token"_ y _"refresh_token"_ mediante las credenciales del usuario
- POST api/auth/refresh/ -- Obtiene un nuevo _"access_token"_ y _"refresh_token"_ mediante un _"refresh_token"_
- POST api/auth/verify/ -- Verifica el estado del _"access_token"_

## Modelo Persona
- GET api/persona/  -- Consulta la lista de personas
- POST api/persona/ -- Crea un nuevo registro de persona
- GET api/persona/:id/ -- Consulta un registro de persona por su id
- PUT api/persona/:id/ -- Edita un registro de persona identificada por su id
- DELETE api/persona/:id/ -- Elimina un registro de persona identificada por su id 

## Modelo Vacuna
- GET api/vacuna / -- Consulta la lista de vacunas
- POST api/vacuna/ -- Crea un nuevo registro de vacuna
- GET api/vacuna/:id/ -- Consulta un registro de vacuna por su id
- PUT api/vacuna/:id/ -- Edita un registro de vacuna identificada por su id
- DELETE api/vacuna/:id/ -- Elimina un registro de vacuna identificada por su id

## Modelo Mascota
- GET api/mascota / -- Consulta la lista de mascotas
- POST api/mascota/ -- Crea un nuevo registro de mascota
- GET api/mascota/:id/ -- Consulta un registro de mascota por su id
- PUT api/mascota/:id/ -- Edita un registro de mascota identificada por su id
- DELETE api/mascota/:id/ -- Elimina un registro de mascota identificada por su id
