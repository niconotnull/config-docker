# Comando básicos de Docker para generar la imagen

1- Crear la imagen y las configuraciones en el archivo Dockerfile
2- Ir al directorio donde se encuentra el Dockerfile
3- Generar el build 

   docker build -t config-server:v1 .

4- Se descarga la imagen base 

5- Validar que se haya creado la imagen

  docker images
  docker image ls

6- Crear una red un network con un nombre especifico, para agregar todos nuestros microservicios

	docker network create springcloud


7- Generar el contenedor a partir de la imagen, el puerto que se asigna el primero se define el puerto externo
   puede ser cualquier puerto, el segundo puerto es el que se establece en el microservicio, es decir el puerto
   propio de la imagen, se le deberá de dar un nombre al contenedor con --name y asignar la red con --network y por
   ultimo el nombre de la imagen

   docker run -p 8888:8888 --name config-server --network springcloud config-server:v1


8- Validar el contenedor:

  http://localhost:8888/microservicio-oauth/dev       


9- Nos muesta la lista de contenedores

 docker container ls 
 docker container ps -a  

10- Detener el contenedor

  docker stop 7923a7382f1f


11 Siguiendo el  log

	docker logs -f (nombre o id)
	docker logs -f 6ae0085814da


Generar contenedor
docker run -p 8888:8888 --name config-server --network springcloud config-server:v1
docker run -p 8761:8761 --name servicio-eureka-server --network springcloud servicio-eureka-server:v1 


# INSTALANDO UNA IMAGEN DE MySQL

1 - docker pull mysql:8       // instalamos mysql la versión 8
   
    docker images

2- Deplegar la instacion de mysql en un contenedor
   (Si se tiene una instancia de Mysql levantada localmente es necesario cambiar el puerto)
   -e instruccion que permite setear variables de entorno

   docker run -p 3306:3306 --name servicio-mysql --network  springcloud -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_DATABASE=bd_examenes -d mysql:8

   docker logs -f  servicio-mysql 


# INSTALANDO UNA IMAGEN DE POSTGRESSQL

1- docker pull postgres:12-alpine

   docker run -p 5432:5432 --name servicio-postgres12 --network springcloud -e POSTGRES_PASSWORD=123456 -e  POSTGRES_DB=db_microservicios_usuarios -d postgres:12-alpine    

    docker logs -f servicio-postgres12 




  






NOTA : cuando se despliega un servicio que apunta a una bd en este caso a la red en donde se alojaron 
   nuestros servicio marcara un error al crear el build, para que maven no realice el test

   mvn clean package -DskipTests


Construimos la imagen para el microservicio-usuarios, ir  al ruta donde se encuentra el Dockerfile
1- docker build -t microservicio-usuarios:v1 .

2- docker images

3. Crear la instancia 
    (se define en -P por que el puerto del servicio es aleatorio, lo genera de forma automatica)
    (No se define --name o el nombre del contenedor por que es opcional por que en ninguna parte los otros
    microservicios haran una referecia al microservicio por que se conecta al servidor de Eureka y al servidor
    de configiración)

   docker run -P  --network springcloud microservicio-usuarios:v1




Lista de Contenedores

docker run -p 3306:3306 --name servicio-mysql --network  springcloud -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_DATABASE=bd_examenes -d mysql:8

validando: psql -U postgres  --\l \c <db name>  \dt <List table>

docker run -p 5432:5432 --name servicio-postgres12 --network springcloud -e POSTGRES_PASSWORD=123456 -e  POSTGRES_DB=db_microservicios_usuarios -d postgres:12-alpine   


docker run -d  -p 8761:8761 --name servicio-eureka-server --network springcloud servicio-eureka-server:v1 
docker run -d  -p 8888:888 --name servicio-config --network springcloud config-server:v1  
docker run -d  -P --name servicio-usuarios --network springcloud  microservicio-usuarios:v1
docker run -d  -P --name servicio-administrador --network springcloud  microservicio-administrador:v1
docker run -d  -p 9100:9100 --name servicio-oauth --network springcloud  microservicio-oauth:v1
docker run -d  -p 8090:8090 --name servicio-gateway --network springcloud  microservicio-gateway:v1

docker build -t microservicio-usuarios:v1 .

escalando una instancia



git remote set-url origin https://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@github.com/niconotnull/config-docker.git















