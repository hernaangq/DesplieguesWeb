# CDPS - Práctica Creativa 2 
# Hernán García Quijano & Eric Ordás Martín & Luis Núñez Casal
 
Este es nuestro proyecto **Práctica Creativa 2** del curso 2023-2024 de la asignatura de CDPS. 

Creación de un escenario completo de despliegue de una aplicación fiable y escalable que integre los diversos contenidos impartidos en la asignatura. Para ello se usarán múltiples tecnologías. Esta práctica está orientada a afianzar los conocimientos adquiridos a lo largo de la asignatura con respecto a los temas relacionados, con el despliegue de aplicaciones en la nube y aplicaciones basadas en microservicios utilizando Docker y Kubernetes. Para ello, se define cinco grandes bloques.

- Despliegue de una aplicación monolítica en una máquina virtual en google cloud.
- Despliegue de una aplicación monolítica usando docker.
- Segmentación de una aplicación monolítica en microservicios utilizando docker-compose.
- Despliegue de una aplicación basada en microservicios utilizando Kubernetes.
- Despliegue de una aplicación basada en microservicios utilizando Helm Charts.


# **1. Despliegue de la aplicación en máquina virtual pesada**
Pasos para arrancarla:
Lo primero será crear una instancia de VM en Google Cloud, configurando una regla FW que permita todo tipo de tráfico.

~~~
cd bloque1
python3 bloque1.py arrancar
~~~
Así nuestra aplicación ya estará corriendo en la IP externa de la máquina en el puerto 9080.

En caso de que queramos especificar otro puerto distinto usaremos lo siguiente:
~~~
python3 bloque1.py arrancarPuerto [puerto]
~~~

Para destruir el escenario usaremos:
~~~
python3 bloque1.py liberar
~~~

# **2. Despliegue de una aplicación monolítica usando docker**
Pasos para arrancarla:
Al igual que en el bloque 1, lo primero será crear una instancia de VM en Google Cloud, configurando una regla FW que permita todo tipo de tráfico. Podemos utilizar la misma instancia que tenemos para el bloque 1 si procede.

~~~
cd bloque2
python3 bloque2.py crear
~~~
Así nuestra aplicación ya estará creada. Posteriormente, la arrancaremos para poder verla en la IP externa. De esta forma debería ser visible desde un navegador.

~~~
python3 bloque2.py arrancar
~~~

Para destruir el escenario usaremos:
~~~
python3 bloque2.py liberar
~~~


# **3. Segmentación de una aplicación monolítica en microservicios utilizando docker-compose**
Pasos para arrancarla:
Al igual que en el bloque 1 y 2, lo primero será crear una instancia de VM en Google Cloud, configurando una regla FW que permita todo tipo de tráfico. Podemos utilizar la misma instancia que tenemos para el bloque 1 si procede.

~~~
cd bloque3
python3 bloque3.py
~~~
Así nuestra aplicación ya estará corriendo en la IP externa de la máquina en el puerto 9080.


# **4. Despliegue de una aplicación basada en microservicios utilizando Kubernetes**
Pasos para arrancarla:
Lo primero será crear un Kubernetes Engine en Google Cloud.
Después:
~~~
cd bloque4
kubectl apply -f productpage.yaml
kubectl apply -f details.yaml
kubectl apply -f ratings.yaml
kubectl apply -f reviews-svc.yaml
kubectl apply -f review-<version>-<tipo>.yaml
~~~
Usaremos el fichero yaml de v1, v2 o v3, dependiendo de cual versión queramos usar

Para comprobar que los distintos servicios y deployments se han cargado correctamente, podemos usar el siguiente comando:
~~~
kubectl get all
~~~

Y en caso de que queramos liberar el escenario usaremos:
~~~
kubectl delete --all deployments && kubectl delete --all pods && kubectl delete --all services
~~~

Así nuestra aplicación ya estará corriendo en la IP externa de la máquina en el puerto 9080.


# **Opcional. Despliegue de la aplicación con Helm Charts**
Pasos para arrancarla:

Trabajaremos con GKE ya que tiene instalado Helm de manera predeterminada.
Para poder desarrollar el proyecto realizaremos lo siguiente:

~~~
helm create <nombre que queramos, por ejemplo: prueba>
cd prueba
~~~
Una vez realizado esto, helm ya habrá creado de manera automática todo lo necesario para lanzar la aplicación si quisiéramos con Kubernetes. Dentro encontraríamos los archivos:
- Charts
- Charts.yaml
- Templates
- values.yaml

Una vez copiados dentro de la carpeta templates todos los YAML de nuestra aplicación y editado el archivo de values.yaml para saber desde que repositorio debe arrancar la misma y en qué puerto debe hacerlo; ejecutaremos lo siguiente dentro del directorio de prueba:

~~~
helm install prueba .
~~~

Esperaremos a que la aplicación sea lanzada y podremos visualizarla desde nuestro navegador desde la IP externa que nos dé el balanceado de cargas.
Podemos visualizar qué IP es mediante:
~~~
kubectl get services
~~~

Y podemos visualizarlo todo desde el navegador con: 

~~~
http://<IP externa>:9080/productage
~~~

Por último para borrar todo:

~~~
kubectl delete --all deployments && kubectl delete --all pods && kubectl delete --all services
~~~


# **Información de contacto:**

**Hernán García Quijano:** <hernan.garcia.quijano@alumnos.upm.es>

**Eric Ordás Martín:** <e.ordar@alumnos.upm.es>

**Luis Núñez Casal:** <luisignacio.nunez@alumnos.upm.es>

