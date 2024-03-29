# Ejercicio 3

> Realizado por Lucía Marrón Díaz

[TOC]

## Apartado 1

Crea una red bridge redbd.

```bash
sudo docker network create redbd
```

![image-20240228103835957](./Ejercicio3Luc%C3%ADa.assets/image-20240228103835957.png)

## Apartado 2

Crea un contenedor con una imagen de mariaDB que estará en la red redbd . Este
contenedor se ejecutará en segundo plano, y será accesible a través del puerto 3306. (Es
necesario definir la contraseña del usuario root y un volumen de datos persistente).

```bash
sudo docker run -d --name mysql-container --network redbd -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v mysql-data:/var/lib/mysql mariadb
```

![image-20240228103835957](./Ejercicio3Luc%C3%ADa.assets/image-20240228105120328.png)

Este comando asigna un nombre al contenedor (mysql-container), que estará conectado a la red "redbd" mapeando el puerto 3306. Su contraseña será root para el usuario por defecto (que también es root) y creará un volumen (mysql-data) para persistir los datos.

Comprobamos que el contenedor se ha creado correctamente:

```bash
sudo docker ps
```

![image-20240228103835957](./Ejercicio3Luc%C3%ADa.assets/image-20240228105353693.png)

## Apartado 3

Crear un contenedor con Adminer que se pueda conectar al contenedor de la BD.

```bash
sudo docker run -d --name adminer-container --network redbd -p 8080:8080 adminer
```

![image-20240228103835957](./Ejercicio3Luc%C3%ADa.assets/image-20240228105957462.png)

Comprobamos que ambos contenedores estén creados correctamente:

![image-20240229213433731](./Ejercicio3Luc%C3%ADa.assets/image-20240229213433731.png)

## Apartado 4

Comprobar que el contenedor Adminer puede conectar con el contenedor mysql abriendo un navegador web y accediendo a la URL: http://localhost:8080.

Se ha tenido que liberar el puerto, ya que estaba siendo utilizado por otro proceso de ejercicio anteriores:

Con estos comandos vemos los procesos que estan en el puerto 8080 y la hora a la que han sido creados

```bash
sudo lsof -i :8080
ps -p <PID> -o lstart
```

Por último, detenemos el proceso que no estamos utilizando:

```bash
sudo kill -9 <PID>
```

![image-20240229213433731](./Ejercicio3Luc%C3%ADa.assets/image-20240228110555606.png)

Cubrimos todos los datos de nuestro servidor:

![image-20240229204222911](./Ejercicio3Luc%C3%ADa.assets/image-20240229204222911.png)

#### Vista BD Adminer

![image-20240229204140604](./Ejercicio3Luc%C3%ADa.assets/image-20240229204140604.png)

#### Creación BBDD nueva

Para este paso presionamos "Crear Base de datos" e introducimos el nombre, en nuestro caso: `bbddluciavictor`.

![image-20240229204324712](./Ejercicio3Luc%C3%ADa.assets/image-20240229204324712.png)

#### Comprobación BBDD

Para comprobar si la base de datos se ha creado correctamente, accedemos a la ventana `Comando SQL` y escribimos `SHOW DATABASES`:

![image-20240229204511827](./Ejercicio3Luc%C3%ADa.assets/image-20240229204511827.png)

#### Borrado de contenedores, red y volumen

```bash
sudo docker stop mysql-container adminer-container
sudo docker network rm redbd
sudo docker volume rm mysql-data
```

![image-20240229205954547](./Ejercicio3Luc%C3%ADa.assets/image-20240229205954547.png)

![image-20240229210045590](./Ejercicio3Luc%C3%ADa.assets/image-20240229210045590.png)

#### Comprobación de borrado correcto

```bash
docker ps
docker network ls
docker volume ls
```

![image-20240229210228268](./Ejercicio3Luc%C3%ADa.assets/image-20240229210228268.png)