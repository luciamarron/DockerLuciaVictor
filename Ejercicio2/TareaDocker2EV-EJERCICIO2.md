## Ejercio 2 - Portainer

##### Se descarga Portainer usando este comando :

```bash
victor@dockerej2:~$ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```
*Usamos las opciones -d, -p y -v en el comando docker run. La opción -d,  que corresponde a --detach, se utiliza para ejecutar el contenedor en  segundo plano. La opción -p, que representa --port, especifica el  puerto; en este caso, el '9000'. Por último, la opción -v, que significa --volumenes, se refiere a la ruta de montaje del volumen de Docker. En  este caso, es /var/run/docker.sock, que es el socket del host, y  /var/run/docker.sock, que es el socket del volumen.* 

![image-20240226101829124](.assets/image-20240226101829124.png)



Accedemos a Portainer desde `http://192.168.56.104:9000` en la maquina cliente. 

![image-20240226102847154](.assets/typora-user-images/image-20240226102847154.png)



##### Muestra contenedores activos, para un contenedor, borra un contenedor:

*Voy a hacer pull de 2 contenedores aleatorios que voy a buscar en dockerhub para hacer la prueba.*

![image-20240227172556466](.assets/image-20240227172556466.png)

![image-20240227172634589](.assets/image-20240227172634589.png)

```bash
victor@dockerej2:~$ sudo docker pull mysql && sudo docker pull postgres
```

*Ahora que estan descargados los 2 contenedores, podemos hacer la prueba.*

```bash
 sudo docker run -d --name mi_postgres -e POSTGRES_PASSWORD=1234 -p 5432:5432 postgres &&  sudo docker run -d --name mi_mysql -e MYSQL_ROOT_PASSWORD=1234 -p 3306:3306 mysql
```

*El parametro `-e` se usa para establecer variables de entorno dentro del contenedor para ajustar configuraciones, en este caso la configuracion de la contraseña de las dos DB es crucial para que el contenedor funcione como es debido.*

![image-20240227172711031](.assets/image-20240227172711031.png)

*Hay 3 contenedores, 1 de ellos es el propio `Portainer`.*

*Paramos `mysql`.*

![image-20240227173418933](.assets/image-20240227173418933.png)

![image-20240227173150845](.assets/image-20240227173150845.png)



*Borramos `postgres`.*

![image-20240227173240273](.assets/image-20240227173240273.png)

![image-20240227173331962](.assets/image-20240227173331962.png)



##### Muestra alguna operación con redes Docker:

*El unico contenedor con una conexion es el propio contenedor de `Portainer` que se llama `vigorous_hugle`.*

![image-20240227173630789](.assets/image-20240227173630789.png)

*Detalles de la conexion del contenedor.*

![image-20240227173723188](.assets/image-20240227173723188.png)

![image-20240227180403058](.assets/image-20240227180403058.png)

*Creamos una conexion nueva.*

![image-20240227180437849](.assets/image-20240227180437849.png)



##### Muestra alguna operación con volúmenes Docker:

![image-20240227175121303](.assets/image-20240227175121303.png)

*Aqui se muestran los tres volumenes docker uno de ellos con el estado `unused` ya que eliminamos el contenedor de postgres en el primer ejercicio y el volumen esta pendiente de ser adjudicado.*

 *(tiene esos nombres porque no cree ningun volumen a mano con -v al hacer el docker run asi que los autogenera con nombres aleatorios).*

![image-20240227180143715](.assets/image-20240227180143715.png)

*Creo un volumen desde `Portainer`.*

![image-20240227180524332](.assets/image-20240227180524332.png)

