## Descripcion
El repositorio es un ejercicio de DevOps que automatiza la construcción de un entorno, realiza pruebas automáticas, entrena un modelo de Maching Learning con un dataset llamado Adult Income y lo despliega el modelo en un servicio web con docker y fastapi

## Estructura
El proyecto se divide en los siguientes directorios:

- .github/workflows
    En este directorio se guardan los workflows que se van a ejecutar en github actions. Dentro tenemos los siguientes archivos:
    * build.yml.- Descarga el dataset , lo compila y lanza los test de forma individual (model_test).
    * integration.yml.- Este workflow comprueba que todo el sistema funciona bien (unit_test)
    * deploy.yml.- Despliega el modelo creando una imagen Docker y lanza el servicio de FastAPI

- src
    Contine los archivos para cargar los datos, entrenar el modelo y evaluar el rendimiento

- unit_test
    Contiene el código para testear las funciones principales como son la carga y procesamiento de datos, el entrenamiento y la evaluación

- model_test
    Contine el codigo que valida el modelo unicamente

- deployment
    Contiene la aplicación en FastAPI y el archivo para generar la imagen de docker

- scripts
    Contiene scripts para registrar el modelo y realizar una petición de prueba

- models
    Se almacenan los modelos entrenados (estos se descargan en la ejecución)

- data
    Contiene los dataset utilizados (estos se descargan en la ejecución)

## Resumen DevOps
1. Cuando se hace un push a la rama Main se ejecuta el workflow buil.yml que instala las dependendencias, descarga los dataset y ejecuta los test dle modelo
2. Cuando se hace una pull request para integrar en Main se ejecuta el workflow integration.yml
para comprobar que la integración es correcta.
3. De forma manual lanzamos el workflow deploy.yml que crea un contenedor en Azure, construye una imagen docker de la aplicacion y la sube a Azure. Después la ejecuta y puede ser utilizada 
  