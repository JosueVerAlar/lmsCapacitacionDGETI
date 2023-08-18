# LMS CAPACITACION DGETI
Este proyecto es una plataforma de aprendizaje autónomo desarrollada para la actualización docente siguiendo la misma vertiente de mejora continua e innovación continua para la Dirección General de Educación Tecnológica, Industrial y de Servicios (DGETI). A continuación se describe de forma detallada el procedimiento para tal objetivo.

## Preparación del ambiente de trabajo
### Cosas a tomar en cuenta:
```
- Archivo "docker-compose.yml"
- Repositorio en github, o una ruta dentro de un servidor o servicio donde se
  crearán los archivos dentro del ambiente de desarrollo
- Tener instalado Docker
- Tener instalado Composer

***Este proyecto está desarrollado en Ubuntu, una versión de Línux***
```
### Preparación de archivo docker-composer
El primer paso es ubicar la carpeta donde se van a alojar todos los archivos que se van a usar. Una Vez hecho eso, se procede a abrir una terminal y nos ubicamos en el path de la carpeta que será usada.Ya ahí crearemos un nuevo archivo mediante el siguiente comando: (vi es para editar, pero si no existe el achivo, lo crea)
```
vi docker-compose.yml
```

*En caso de ser necesario eliminar un archivo, ejecuta el siguiente comando: (sudo es para dar permisos de administrador, rm es para remover, -r significa recursivo, es decir, que haga lo mismo para todo lo que haya en la carpeta pero con el mismo nombre. docker-compose-yml es el nombre del archivo que se va a eliminar. Normalmente cuando hay varios archivos con nombres similares que quieren borrarse, al final de los carácteres que tienen en común se agrega un asterisco.
```
sudo rm -r docker-compose.yml
```

Para verificar que se haya creado el nuevo archivo, ejexcuta el siguiente comando
```
ll
```

Para entrar a editar el archivo usa el siguiente comando:
```
vi docker-compose.yml
```

y para comenzar a editar presiona la tecla ***"insert".***

Para borrar oprime la tecla ***d***
Para pegar oprime ***ctrl*** + ***shift*** + ***v***

Debido a que moodle requiere algunas configuraciones iniciales para iniciar correctamente, es importante revisar el siguiente link [moodle Bitnami](https://hub.docker.com/r/bitnami/moodle), ya que ahí se detallan elementos necesarios de accesos y otras configuraciones. En particular, se requiere agregar los siguientes campos al archivo "docker-compose.yml":
```
moodle:
  ...
  environment:
    - MOODLE_PASSWORD=my_password

    - MOODLE_DATABASE_USER=bn_moodle
    - MOODLE_DATABASE_NAME=bitnami_moodle
    - ALLOW_EMPTY_PASSWORD=yes <-----------------------Elimina este cuando se traslade a producción el proyecto, así como cualquier otro "allow empty password"

    ***PARA AGREGAR EL SMTP***
    - MOODLE_SMTP_HOST=smtp.gmail.com
    - MOODLE_SMTP_PORT=587
    - MOODLE_SMTP_USER=your_email@gmail.com
    - MOODLE_SMTP_PASSWORD=your_password
    - MOODLE_SMTP_PROTOCOL=tls
```

Una vez que termines de editar presiona la tecla ***esc*** para salir del modo edición y escribe ***:wq*** para guardar los cambios

Para iniciar los contenedores con el proyecto, escribe el siguiente comando en la terminal: (esto iniciará los contenedores y creará las carpetas "moodle", "moodledata" y "mariadb")
```
docker compose up -d
```

Para ver la lista de los contenedores creados escribe lo siguiente:
```
docker ps -a
```


## Errores comunes
### No hay variables de entorno declaradas en el archivo .yml
![No hay variables de entorno declaradas en el archivo .yml](https://github.com/JosueVerAlar/lmsCapacitacionDGETI/assets/96144916/d16fe6e2-c89f-469c-aa70-b8b9d8847b7f)
Este error normalmente se da cuando no se definen los password necesarios para que la base de datos de mariaDB se pueda iniciar correctamente. Se soluciona entrando al siguiente link [mariaDB Bitnami](https://hub.docker.com/r/bitnami/mariadb) y buscando la definición de las variables que se indican en el error, después se agregan al archivo ***docker-compose.yml*** para que se configuren desde él nuevamente y se vuelve a usar el siguiente comando para actualizar:
```
docker compose up -d
```

### Error al conectar moodle con la base de datos 
![error al conectar moodle a base de datos](https://github.com/JosueVerAlar/lmsCapacitacionDGETI/assets/96144916/ffd67415-fb57-4802-a1f7-273754909a56)

