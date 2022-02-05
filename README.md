# djRefugioAnimalesSimpleJWTAPI
Aplicación servidor del proyecto [djRefugioAnimalesSimpleJwtClient](https://github.com/fernandoperezwh/djRefugioAnimalesSimpleJwtClient), es necesario ejecutar ambos proyectos para su correcto funcionamiento.

En este proyecto se muestra la autentificacion por tokens utilizando Simple-JWT conforme a la documentación paquetes de terceros de django-rest-framework

# Instalación
- Elegir una directorio de facil acceso para clonar el proyecto. 
    ```bash
    cd ~/Escritorio/
    ```
- Clonar el proyecto ya sea por ssh o https
    ```bash
    # Clone via ssh
    git clone git@github.com:fernandoperezwh/djRefugioAnimalesSimpleJWTAPI.git
    # Clone via https
    git clone https://github.com/fernandoperezwh/djRefugioAnimalesSimpleJWTAPI.git
    ```
- Crear un entorno virtual utilizando python 2.7
    ```bash
    mkvirtualenv djRefugioAnimalesSimpleJWTAPI -p=2.7
    ```
- Activar el entorno creado en el anterior paso
    ```bash
    workon djRefugioAnimalesSimpleJWTAPI
    ```
- Instalar las dependencias del archivo `requirements.txt` 
    ```bash
    pip install -r requirements.txt
    ```
- Realizar las migraciones del proyecto 
    ```bash 
    python manage.py migrate
    ```
- Opcionalmente puede crear un nuevo super usuario con el siguiente comando
    ```bash
    python manage.py createsuperuser
    ```    
    Igualmente puede usar las siguientes credenciales de un superusuario de prueba existente
    - user: `fernando`
    - passwd: `fernando123`

- Finalmente, ejecute el proyecto
    ```bash
    python manage.py runserver
    ```
