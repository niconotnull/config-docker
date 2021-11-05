Que es Kubernetes

Docker permite correr las aplicaciones de una forma contenerizada es decir permite crear imagenes para crear
contendores, esa imagen se puede mover en cualquier maquina y levantar la aplicación con un entorno con 
todas las libreías y archivos que se necesitan dentro de una imagen.

Los contenedores se pueden correr de forma local y en servidores, pero que pasa cuando tenemos muchos 
contenedores poder manejarlos se vulve complejo y para ello necesitamos un orquestador,
Kubernetes es un orquestador que permite manejar nuestras  aplicaciones dentro de contenedores a través 
de muchos servidores esos servidores pueden ser fisicos o virtuales, kubernetes es una herramienta de orquestación de contenedores fue creada por google y es open source.

El principal problema que resuelve kubernetes es la posibilidad de manejar muchos contenedores a través de muchos nodos, proporciona alta disponibilidad, la forma en que kubernetes brinda alta disponibilidad
es a través de la creación de replicas de la aplicación es decir pueder tener varias copias de tu aplicación y si una de esas deja de funcionar kubernetes te va a madar a la que esta funcionando, todo esto de forma transparente para el usuario que esta visitando tu aplicación.

También te permite escalar o crear copias de tu aplicación en el caso de que se tenga más trafico o por el echo de que se requiera tener más capacidad para recibir ese tráfico, también se ecarga de reaizar el recovery  ya que es muy fácil volver a crear las aplicaciones que se murierón por que todo es basado en manifiestos declarativos.


Arquitectura Kubernetes

Kubernetes basicamente tiene dos grandes grupos los MASTER y los WORKER cada worker corre un agente de kubernetes llamado KUBELET en los master tenemos varios componentes entre ellos esta 

API SERVER:  es la que se encrga de exponer una interfaz para que diferentes clientes puedan interactuar 
con kubernetes por ejemplo: interfeces web, clientes APi,  o cliente de kubernetes que se llama KUBECTL

CONTROLLER MANAGER: es el que maneja lo que pasa en el cluster es todo el timpo al tanto que los contenedores
estén corriendo y que contenedores deben de estar corriendo.

SCHEDULER: permite recibir recibir las ordenes del controller maneger y mueve los pods de lugar e lugar
todo este proceso se gurda en una base de datos llamado ETCD.

ETCD: es una base de datos que tiene la información del estado del cluster, tambien tiene toda la información y todas las configuraciones del cluster y los nodos o los workers es donde que es donde se corren los pods de la aplicación

Que es un POD

Un pod es un set de contenedores que comparten el namespace de red, lo más normal es correr un solo contenedor en cada pod pero hay casos donde se corren más de uno ya que se puede dividir algunas tareas
lo que hay que tener en cuenta es que estos pods son valatiles por ejemplo cuando realizamos un nuevo deploy para cambiar la version los pods se destrullen y se crean nuevos.


A través de todos los nodos o WORKER´S se tiene una OVERLAY NETWORK que lo que permite es compartir una red entre todos los pods no importa en que nodo esten entonces el pod A, puede llegar al pod B por más que esten en diferentes nodos, no es buena idea aputar a la ip de un nodo ya que son volatiles. Lo que se realiza comunmente es crear un servicio de kubernetes, tipos de servicios:

CLUSTER IP: Servicio que se caracteriza por tener una ip que nunca cambia, entonces en lugar de un pod a pod
se va de un pod a un servicio ese servicio tiene como backend los pods que corre tu aplicacion, el servicio
encuentra ese pod basado en un set de reglas o etiquetas que se ponen a los pods para que el servicio  los pued encontrar

NODE PORT: Permite crear un puerto en el nodo que va a llegar a tu tráfico, permite 

INGRESS: Permite cear reglas basadas por ejemplo en el subdomino

LOAD BALANCER: permite crear un balanceador de carga en tu provedor 



Kubernetes se maneja con manifiestos declarativos por ejemplo se puede crear un manifiesto que tenga un template de una aplicación en particular  a este tipo de template se le dice deployment, el deployment es un template para  crear pods una vez que vas aplicar este template en el cluster de kubernetes el CONTROLLER MANAGER se encargará de crear esos PODS en el cluster.






















