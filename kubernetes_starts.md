##Kubernetes

#Kubernetes permite orquestar los contenedores

Resumen
Kubernetes es declarativo es decir se crea un manifiesto es decir un deployment donde se le solicita a kubernetes que levante un pod donde se definen los contenedores cuantas replcias se requieren, este maniefiesto se pasa a la API de kubernetes y kubernete va a trata en los posible de ejecutar lo que se le pide en el manifiesto es dicir si se le piden tres contenedores va a tratar de distribuirlos en los workers, estos workers son los que van a correr nuestras aplicaciones, estos contenedores son manejados por unos servicios de kubernetes en especial es el servicio de SHEDULE que es el que se encarga de mover esos contenedores de un lugar a otro y se conecta a la api de kubernetas estos workers se concetan a la api de kubernetes a través de un agente que se llama kubelet que es un servicio de kubernetes que nos permite conectar todos los workers  y todos lo servicios de kubernetes entre si.

Si alguno de esos workers o algun contenedor se cae sabe que no esta cumpliendo con lo que tiene que cumplir va a tratar de arreglar ese problema automaticamente va a mover ese contenedor a otro worker

Instalar minikube
Permite instalar el cluster de kubernetes, minikube crear una maquina virtual donde se instala todos los componentes de kubernetes

1. minikube start : Iniciar el cluster
2. kubectl get po -A : Permite interactuar con el cluster
3. kubectl get nodes : Muestra los nodos del cluster de kubernetes
4. kubectl --help
5. kubectl config get-contexts : muestra los cotextos que estan en archivo de configuracion de kubectl


Recursos de Kubernetes
1. namaespace: es una divición logíca de tu cluster esto permite separar la carga en tu cluster de kubernetes
   permite didir el tráfico de alguna forma, es decir dividir los recursos de alguna forma

  1. kubectl get ns : muestra los namespace por defecto que vienen con cualquier cluster
  2. kubectl -n kube-system get pods : permite ver los pods que corren de kube-system es decir los pods de sistemas
  3. kubectl -n kube-system get pods -o wide : muestra información adicional
  4. kubectl -n kube-system delete pod  kube-proxy-6r8m2 : eliminando un pod y validando la replicacion de un pod, es decir kubernetes realiza la replicación automaticamente de ese pod, por que ha si esta definido en el template, se crea un nuevo pod cuando se elimino el anterior  



Levatando un cluster de kubernetes
1. Instalar kubectl, es un cliente de kubernetes es el cliente que se conecta al cluster de kubernetes
2. kubectl version --client=true  :Muestra la version


Levantando nuestro primer pod
1. vim 01-pod.yaml : validando el manifiesto de un pod muy simple, muestra lo siguiente
   1. apiVersion : Se define la version de la api del recurso de kubernetes
   2. metadata name : se define el nombre del pod
   3. spec containers :  se declaran los contenedores que correran dentro del pod, todos lo contenedores que corran dentro del pod compartiran la ip
2. kubectl apply -f 01-pod.yaml : Ejecutamos el manifiesto para crear el pod
3. kubectl get pods
4. kubectl exec  -it nginx  -- sh : Entramos a la terminal del contenedor 
5. kubectl  delete pod  nginx : Eliminamos un pod pero no levanto replicas

5.  vim 02-pod.yaml : Este manifiesto contiene mas informacion  
    1. env name value : permite definir variables de entorno, permite mandar configuraciones al contenedor
    2. env name DD_AGENT_HOST : permite obtener el valor de otro lado, 
    3. resources : permite asignar recursos al contenedor
    4. resources request : permite garantizar los recursos del contenedor
    5. resources limits : limite de recursos que este pod puede llegar a tener
    6. redinessProbe : Permite decirle a kubernetes que el pod esta listo para recibir tráfico, 
    7. livenessProbe : Permite decirle a kubernetes que el pod esta vivo
    8. ports : Define el tipo de puerto donde queremos escuchar

6. kubectl apply -f  02-pod.yaml : Ejecutamos un nuevo pod
7. kubectl get pods
8. kubectl get pod nginx  : Permite ver el estado del pod
9. kubectl get pod nginx  -o  yaml


Nota: no deberiamos de deployar pods, sino deberiamos de deployar deployments
      UN DEPLOYMENT ES UN TEMPLATE PARA CREAR PODS, se defininen las replicas que es la cantidad de pods que necesitamos de nuestro deployment


1. kubectl  delete pod  nginx 
2. vim 04-deployment.yaml
3. kubectl apply -f  04-deployment.yaml 
4. kubectl get pods : Validamos que ahora tenemos dos pods
5. kubectl  delete pod nginx-deployment-7558575c69-m7v46 : Validamos el delete de un pod y validamos que kubernetes levanta un nuevo pod por que así lo definimos en el manifiesto de que se requieren dos replicas de ese contenedor
6. kubectl delete -f 04-deployment.yaml : Eliminamos el deployment

7. kubectl apply -f 03-daemonset.yaml : Se define un template para que el pod se ejecute o corra en cada nodo kind: DaemonSet
8. kubectl get pods -o wide































