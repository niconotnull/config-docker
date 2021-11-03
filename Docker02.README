Curso platzie docker 29/10/2021 20:29hrs 

1- docker rename servicio-eureka-server servicio-eureka-server-2
2- docker ps -a
3- docker ps
4- docker rm <id,name_image>  --Elimina un contenedor
5- docker container prune     --Elimina todos los contenedores que se encuntran detenidos 
6- docker rm -f <id_contenedor> --Detiene y elimina un contenedor
7- docker run --name proxy -p 8080:80  nginx    -- -p define el puerto externo e interno puerto externo es el puerto al que se accede desde la maquina puerto interno es el puerto del contenedor
8- docker run --name proxy -d -p  8080:80 nginx --corre el contenedor en modo
9- docker logs <contenedor> --Vemos los logs que existen
10- docker logs -f <contenedor> --Entramos directamente al log
11- docker logs --tail 10  -f <contenedor>
12- docker run --rm -p 3000:3000 <contenedor>       --Cuando este contenedor se detenga borralo no quiero conservarlo



Instalar Ubuntu
1- docker run ubuntu
2- docker ps -a 
3- docker -it ubuntu (Ejecuta ubuntu y accede al shell de ubuntu)  -i: interactivo -t: abrir consola
4- cat /etc/lsb-release
5- exit  --Salir de ubuntu
6- docker run --name alwaysup -d ubuntu tail -f /dev/null  --Permite ejecutar el contenedor de ubuntu hasta especifar la detencion
7- docker exec -it alwaysup bash    --permite conectarnos a un contenedor que se esta ejecutando actualmente
8- docker inspect --format '{{.State.Pid}}' alwaysup  --format --Matar el proceso
9- kill <id>  -- nativamente en linux funciona en mac no jejeje
10- docker stop alwaysup --este si funciona para matar un proceso en mac
11- 


Ciclo de vida de un contenedor
1- Cada vez que un contenedor se ejecuta, se esta ejecutando un proceso del sistema operativo, es el proceso principal del contenedor
2- Un contenedor se ejecuta siempre y cuando su proceso principal se este ejecutando, cuando un proceso falla o se detetiene
   de un contenedor, ese proceso se va a detener
3- Cuando ejecutamos un contenedor podemos especificar el comando con el que corra  
4- Mientras el proceso principal(main process) de un cotenedor este corriendo el contenedor estará corriendo


Exponiendo Contenedores
1- Como funciona un contenedor desde afuera
2- docker run -d
3- docker run --name proxy -d -p  8080:80 nginx --corre el contenedor en modo
4- docker logs <contenedor>
5- docker logs -f <contenedor>
6- docker logs --tail 10  -f <contenedor>

Manejo de datos en Docker con MongoDB
1- mkdir dockerdata
2- ls -lac
3- cd
4- docker run -d --name servicio-mongo  mongo
5- docker exec -it servicio-mongo bash
6- ll     --verificamos el contenido del contenedor
8- mongo  --nos conectamos a la bd
9- show dbs
10- use platzi
11- db.users.insert({"nombre": "Nicolas" })
12- db.users.find()




Compartir datos entre el contenedor y la máquina anfitrion(Bind Mount)
1- Crear un directorio en la máquina anfitrion que tenga una versión de alguna información del contenedor es decir
   que lo que pasa dentro del contenedor ocurra tambien en la máquina anfitrion, ejemplo de datos con mongo
   Bind Mount: guarda los archivos en la máquina local persistiendo y visualizando los datos lo cual no es seguro


2- Tener claro que directorio queremos montar sobre el contenedor

	1- mkdir mongodata
	2- docker run -d  --name servicio-mongo -v /Users/JNicolas/Documents/dockerdata/mongodata:/data/db  mongo   --Con -v definimos que se realizará un bytemount 
	3- docker exec -it servicio-mongo bash
	4- ll
	5- mongo
	6- use platzi
	7. db.users.find()
	8- docker rm -f <contenedor>
	9- ahora validamos que aunque se haya eliminado el contenedor los datos que se insertarón en bd ahora los tenemos
	   disponibles en el directorio que se definio previamente en el contenedor.

	10- Si ahora ejecutamos un nuevo contenedor montando este directorio donde se encuentra la información de la bd 
	11- docker run -d  --name servicio-mongo -v /Users/JNicolas/Documents/dockerdata/mongodata:/data/db  mongo
	12- docker exec -it servicio-mongo bash
	13- mongo  
    14- use platzi
    15- db.users.insert({"nombre": "Nicolas" })
	15. db.users.find()	


Volumnes, manejos de volumenes (es mejor que la otra opcion jeje)
Volume: Guarda los archivos ene el area de Docker donde el mismo los adminsitra es seguro

1- docker volume ls              --Vemos los volumenes disponibles
2- docker volume create dbdata   --Creamos un nuevo volumen
3- docker volume ls 
4- Crear un nuevo contenedor y montar el volumen para que se escriban los datos como se realizo previamente
5- docker run -d --name servicio-mongo --mount src=dbdata,dst=/data/db mongo 
6- docker inspect servicio-mongo  
6- docker exec -it servicio-mongo bash
7- use platzi
8- db.users.insert({"nombre": "Nicolas" })
9- db.users.find()
10- docker rm -f servicio-mongo  --Eliminamos el contenedor
11- docker run -d --name servicio-mongo --mount src=dbdata,dst=/data/db mongo --ejecutamos el contenedor con el mismo volumen 


TMPFS Mount
Guarda los archivos temporalmente y persiste los datos en la memoria del contenedor

1- touch prueba.txt 
2- cat prueba.txt
3- docker run -d --name copytest ubuntu tail -f /dev/null
4- docker exec -it copytest bash
5- ll
6- mkdir testing
7- Copiar el archivo prueba.txt que se encuentra en la máquina anfitrion al contenedor
8- docker cp prueba.txt copytest:/testing/test.txt
9- docker exec -it copytest bash --validar
10- Extraer el archivo del contenedor a la máquina anfitrion
11- docker cp copytest:/testing localtesting   	
12- ls validamos que ahora el contenido de la carpeta testing del contenedor ahora se encuentra en el directorio de localtesting


CONCEPTOS FUNDAMENTALES DE IMAGENES

Las imagenes son plantillas o moldes de las cuales docker contrulle contenedores
Cada vez que se crea un contenedor docker utiliza una imagen

1- docker image ls 
2- docker pull ubuntu:20.04    -pull permite traer una imagen desde un repositorio externo hacia mi máquina 


Crear propias imagenes


1- mkdir imagenes
2- touch Dockerfile
3- docker build -t ubuntu:platzi .  --Instruccion que se le pide a docker construir una imagen   
4- Correr un nuevo contenedor a partir de la imagen que se creo
5- docker run -it ubuntu:platzi
6- Publicar una image
7- docker login
8- docker tag ubuntu:platzi haydenick/ubuntu:platzi   
9- docker push haydenick/ubuntu:platzi                      
10- docker history ubuntu:platzi  --permite ver la informacion de como se construye cada capa 


Administrando

1- docker ps -a
2- docker container prune --Permite matar solo los contenedores que estan detenidos
3- docker rm -f $(docker ps -aq)    --Permite matar todos los cotenedores
4- docker network ls
5- docker volumn ls
6- docker network prune
7- docker volumen prune
8- docker system prune -- Elimina todos los contenedores, network y volumenes detenidos, images
9- docker run -d --name  app --memory 1g platizapp  --Permite evaluar escenarios de ejecucion manejando la memoria y los recursos
10- docker inspect app
11- docker stats


13- docker ps -q   --obtener los id
14- docker stop $(docker ps- q)  --Detener todos los contenedores 


Deteniendo contenedores correctamente
1- cd a





