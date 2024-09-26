# moduloInicialSGE
creacion de un modulo en odoo

-Para empezar creamos una carpeta llamada docker-compose, dentro de ella creamos tres carpetas llamadas: config_odoo, dev-addons y log.

-Dentro de la carpeta docker-compose pondremos el archivo docker-compose.yml con la siguiente codigo:

-version: '3.1'
-services:
  web:
    image: odoo:17.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - odoo-web-data:/var/lib/odoo
      - ./config_odoo:/etc/odoo
      - ./dev-addons:/mnt/extra-addons
      - ./log:/var/log/odoo
    environment:
      - HOST=db
      - USER=odoo
      - PASSWORD=odoo
  db:
    image: postgres:latest
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - odoo-db-data:/var/lib/postgresql/data/pgdata
    
volumes:
  odoo-web-data:
  odoo-db-data:
  
-Como podemos comprobar en la etiqueta volumenes vienen los nombres de las carpetas que hemos creado que podrian llamarse de otra forma y cambiar el nombre en el codigo del archivo.

-Como siguiente paso debemos colocar el archivo odoo.conf dentro de la carpeta config_odoo con el siguiente codigo:

-[options]
addons_path = /mnt/extra-addons
data_dir = /var/lib/odoo
admin_passwd = diana
-logfile = /var/log/odoo/odoo-server.log

-En este codigo es importante cambiar la contraseña si lo deseamos cada vez que creemos un nuevo modulo.

-Despues de tener nuestras carpetas preparadas abrimos el power shell de nuestro ordenador como administradores con cd y la ruta de nuestra carpeta creada cd C:\Users\Diana\Desktop\SISTGESTEMPR FRAN\TEMA2\docker--compose y ejecutamos el comando Docker compose up.

-Se crearian los containers en la aplicacion Docker hay un container que se llama web-1 que al lado viene en azul el puerto que es el que nos llevara al odoo. 

-Ante debemos pinchar en los tres puntos para abrir el terminal y proceder a crear nuestro modulo.

-Cuando se abre el terminal con los siguientes comandos entramos a la carpeta donde alojaremos nuestro modulo:

-ls
-cd mnt
-ls
-cd extra-addons
-ls
-odoo scaffold dam2 //con este comando y poniendo el nombre de nuestro modulo se crea 
-ls
-dam2

-Despues a travez de la carpeta de docker-compose buscamos nuestra carpeta dev-addons dentro estara la carpeta de nuestro modulo dam2 la abriremos en este caso con el visual studio donde encontraremos el directorio de archivos a modificar para poder abrir nuestro modulo.

-Descomentar el apartado data security del manifest_py
views.xml, descomentar primer párrafo y borrar el field value2 y la actions opening views on models.py.

-Ahora abrimos oddo atraves de docker, (la primera vez tendremos que entrar con la contraseña que pusimos en el archivo odoo.conf)y activamos modo desarrollaror y bucamos nuestro modulo en la barra de busqueda y nos saldra nuestro modulo, en los tres puntos que aparece al lado de nuestro modulo pinchamos y actualizamos y entraremos en nuestro modulo.

  
