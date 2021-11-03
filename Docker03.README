Curso platzie docker 30/10/2021 09:21hrs 

Docker con aplicaciones

1- git clone https://github.com/platzi/docker

------------------------------------------DOCKERFILE-------------------------------------------

FROM node:12

# Copiar todo lo que hay en la carpeta actual
# a la carpteta /usr/src en el contenedor
COPY ["package.json","package-lock.json" , "/usr/src/"]

# Establece el directorio de trabajo  (cd /usr/src) es quivalente pero del contexto del build 
WORKDIR /usr/src


# ya situados en el directorio /usr/src descargargamos las dependencias del proyecto
RUN npm install

COPY ["." , "/usr/src/"]


# Exponer un puerto, permite que el puerto sea vinculable a un puerto de la máquina huesped
EXPOSE 3000


#Comando por defecto que se especifica cuando se corra el contenedor
CMD ["npx", "nodemon", "index.js"]


--------------------------------------------------------------------------------------------------

1- Con este Dockerfile permite construir la imagen para el proyecto
2- docker build -t platziapp .
3- docker image ls  --Validar que la imagen se haya construido
4- Con la imagen definida ahora se puede construir una contenedor

 1- docker run -d --rm -p 3000:3000 platziapp       --Cuando este contenedor se detenga borralo no quiero conservarlo
 2- validar http://localhost:3000/



 Cache

 0- docker run -d --rm -p 3000:3000 platziapp 
 1- docker build -t platziapp . -- Permite buildear la imagen platziapp
 2- docker run --rm -p 3000:3000 -v /Users/JNicolas/Documents/docker/docker/index.js:/usr/src/index.js platziapp


------------------------------------------COMUNICARSE CON OTROS CONTENEDORES-----------------------------------------
Conectandonos a Mongo
¿Como conectar dos contedenores para que se comunuque?

Creando redes virtuales de docker

1- docker network ls
2- docker network create --attachable platzinet --permite crear una nueva red y con attachhable para establecer que otros contenedores se conecten a ella cuando quieran
3- docker inspect platzinet
4- docker network connect platzinet servicio-mongo --conectando nuestro contenedor de mongo a nuestro contenedor de platziapp
5- docker inspect platzinet
6- docker run -d --name platziContainer  -p 3000:3000 --env MONGO_URL=mongodb://servicio-mongo:27017/test platziapp --env con esta instruccion especificamos una variable de entorno
7- docker network connect platzinet platziContainer
8- exito rotundo



------------------------------------------DOCKER COMPOSE-----------------------------------------
Lo que permite hacer es definir de manera declarativa 


version: "3.8"

services:
  app:
    image: platziapp
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"

  db:
    image: mongo

1- Defininir el archivo docker-compose-yml
2- docker-compose up
3- docker-compose up -d
4- docker network ls
5- docker-compose logs  --Permite ver todos los logs de los contenedores definidos el el docker-compose
6- docker-compose logs app  --Permite ver el log de un contenedor particular
7- docker-compose logs -f app
8- docker-compose exec app bash --Mostrar la consola del contenedor
9- docker-compose ps -d
10- docker-compose down  --Permite matar los contenedores y la red que los interconecta


Build
1-  image: platziapp --Con esta instruccion definimos una imagen previamente construida

2-  build -permite construir una imagen a apartir de los archivos que tiene en disco
3- docker-compose build  --Se le pide que realice un build de los archivo del docker-compose
4- docker-compose up -d

5- docker-compose build app --Hacer cambio en el proyecto y refresar 
7- docker-compose up -d


Mejorando el punto 5 y 7 con boun mount

1- Agregar instruccion para regenerar el contenedor automaticamente
volumes:
      - .:/usr/src
      - /usr/src/node_modules   --Se agrego esta instruccion por que no se estan cargando los modulos de node
                                -- se le dice al contenedor que si monta cosas debera de ignorar esta ruta, se define
                                  una ruta dentro del contenedor ques donde estarán los modulos de la imagen cuando se realiza el build, montar nada en esta ruta montar aqui .:/usr/src pero no tocar  nada aqui /usr/src/node_module  

2- docker-compose up -d

3- docker-compose logs -f app        





version: "3.8"

services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"

  db:
    image: mongo



version: "3.8"

services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src
      - /usr/src/node_modules
    command: npx nodemon index.js     

  db:
    image: mongo


trabajando correctamente con docker-compose: al colaborar con un equipo de desarrollo

COMPOSE OVERRIDE
Permite realizar cambio de

1- touch docker-compose.override.yml  --Crear un nuevo archhivo
2- cat docker-compose.override.yml 
3- docker-compose exec app bash --Entrar al contenedor
4- env    --Ver las variables de entorno 
5- docker-compose up -d --scale app=2  --Define que se levntaran dos intancias de app

   Nota: se requiere definir un rago de puertos y que esten diponibles para los contenedores
  ports:
      - "3000-3001:3000"

6- docker-compose down
7- docker-compose up -d --scale app=2 
8- docker-compose ps


mas operaciones
 administrar  o desbloquer
      desbloquer movil 
          





