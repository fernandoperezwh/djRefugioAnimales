# Manual de instalación
- Elegir una directorio de facil acceso para clonar el proyecto. 
    ```bash
    cd ~/Escritorio/
    ```
- Clonar el proyecto ya sea por ssh o https
    ```bash
    git clone git@github.com:fernandoperezwh/djRefugioAnimalesSimpleJWTAPI.git
    ```
    ```bash
    git clone https://github.com/fernandoperezwh/djRefugioAnimalesSimpleJWTAPI.git
    ```
- Crear un entorno virtual. Este proyecto fue elaborado en python 2.7 y por lo tanto debera crear el entorno con esta misma versión
    ```bash
    mkvirtualenv djRefugioAnimalesSimpleJWTAPI -p=2.7
    ```
- Activar el entorno creado en el anterior paso
    ```bash
    workon djRefugioAnimalesSimpleJWTAPI
    ```
- Instalar las dependencias del proyecto que se encuentran en el archivo `requirements.txt` 
    ```bash
    pip install -r requirements.txt
    ```
- Realizar las migraciones del proyecto 
    ```bash 
    python manage.py migrate
    ```
- Para comprobar que todo se encuentre correctamente, intente ejecutar el proyecto.
    ```bash
    python manage.py runserver
    ```

- Cree un nuevo super usuario con el siguiente comando. Sugerimos que recuerde las credenciales de su usuario ya que los usaremos para autentificarnos en el proyecto y consumir los endpoints/recursos.
    ```bash
    python manage.py createsuperuser
    ```    
