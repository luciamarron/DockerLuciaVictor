# DOCKER

> Realizado por Lucía Marrón Díaz

[TOC]

## Configuración inicial

Creación del repositorio en Github y clonación del mismo en el repositorio local a través de GitKraken.

![image-20240223092735461](./Ejercicio1Luc%C3%ADa.assets/image-20240223092735461.png)

![image-20240223092751764](./Ejercicio1Luc%C3%ADa.assets/image-20240223092751764.png)

Creación de la rama para el ejercicio 1, realizada presionando el botón `Branch`.

## ![image-20240223093509805](./Ejercicio1Luc%C3%ADa.assets/image-20240223093509805.png)



## Ejercicio 1 - Servidor de base de datos

### 1.1. Arrancar un contenedor que se llame web y que ejecute una instancia de una imagen con Apache y php.

Este comando ejecuta un contenedor en segundo plano (-d) a partir de la imagen `php:apache`, mapea el puerto 8080 de la máquina host al puerto 80 del contenedor (-p) y le asigna el nombre web (--name).

```bash
sudo docker run -d -p 8080:80 --name web php:apache
```

![image-20240223095001532](Ejercicio1Luc%C3%ADa.assets/image-20240223095001532.png)

Creamos el fichero index.html (que será lo que veamos desde el navegador web) a través del editor `nano`.

```bash
sudo nano index.html
```

![image-20240223095556704](Ejercicio1Luc%C3%ADa.assets/image-20240223095556704.png)

Es necesario presionar Ctrl + O para guardar los cambios antes de salir.

Copiamos el archivo `index.html` al contenedor a través del siguiente comando:

```bash
sudo docker cp index.html web:/var/www/html/
```

![image-20240223095913019](Ejercicio1Luc%C3%ADa.assets/image-20240223095913019.png)

Antes de visualizar el contenido del contenedor en el navegador, comprobamos que el contenedor `web` esté en ejecución:

```bash
sudo docker ps
```

![image-20240223100233926](Ejercicio1Luc%C3%ADa.assets/image-20240223100233926.png)

En caso de que el contenedor no apareciese en esta lista,  sería necesario iniciar el contenedor a través del comando:

```bash
sudo docker start web
```

#### Salida del fichero index.html

Accedemos a la aplicación HTML desde el navegador visitando http://localhost:8080

![image-20240223100755769](Ejercicio1Luc%C3%ADa.assets/image-20240223100755769.png)

#### Salida del script mes.php

Primero creamos el script mes.pho a través del editor Nano:

```bash
sudo nano mes.php

<?php
echo "Hola, este es el mes actual: " . date("F") . "\n";
?>
```

![image-20240228012708630](./Ejercicio1Luc%C3%ADa.assets/image-20240228012708630.png)

Arrancamos el contenedor web

```bash
sudo docker start web
```

![image-20240228013026134](./Ejercicio1Luc%C3%ADa.assets/image-20240228013026134.png)

Copiamos el archivo mes.php en dicho contenedor

```bash
sudo docker cp mes.php web:/var/www/html/
```

![image-20240228013139901](./Ejercicio1Luc%C3%ADa.assets/image-20240228013139901.png)

Accedemos al navegador con la ruta "localhost:8080/mes.php"

![image-20240228013819597](./Ejercicio1Luc%C3%ADa.assets/image-20240228013819597.png)

#### Tamaño del contenedor web

```bash
sudo docker ps -s
```

![image-20240228014009680](./Ejercicio1Luc%C3%ADa.assets/image-20240228014009680.png)

### 1.2. Arrancar un contenedor que se llame bbdd y que ejecute una instancia de la imagen mariadb para que sea accesible desde el puerto 3306.



```bash
sudo docker run -d --name bbdd -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mariadb
```

![image-20240228011506433](./Ejercicio1Luc%C3%ADa.assets/image-20240228011506433.png)

Este comando inicia un contenedor en segundo plano (-d), con el nombre bbdd, mapeando en el puerto 3306 del host al puerto 3306 del contenedor, y estableciendo la contraseña de root como "root" al utilizar la imagen Mariadb.

### 1.3. Establecer las variables de entorno necesarias.

·La contraseña de root sea `root` . 

·Crear una base de datos automáticamente al arrancar que se llame `prueba` . 

·Crear el usuario invitado con la contraseña `invitado` .

Borramos previamente el contenedor `bbdd` para poder añadirle las nuevas variables de entorno a través del comando:

```bash
sudo docker rm bbdd
```

Después, creamos el contenedor de nuevo:

```bash
sudo docker run -d --name bbdd -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e 
MYSQL_DATABASE=prueba -e 
MYSQL_USER=invitado -e MYSQL_PASSWORD=invitado 
mariadb
```

![image-20240228015846929](./Ejercicio1Luc%C3%ADa.assets/image-20240228015846929.png)

#### Instalación del cliente de bases de datos Dbeaver y conexión

![image-20240228020203413](./Ejercicio1Luc%C3%ADa.assets/image-20240228020203413.png)

<img src="./Ejercicio1Luc%C3%ADa.assets/image-20240228021100417.png" alt="image-20240228021100417" style="zoom: 80%;" />

Aquí podemos comprobar que se ha creado correctamente la base de datos llamada '`prueba`'.

#### Borrado de la imagen mariadb

```bash
sudo docker rmi mariadb
```

![image-20240228021357079](./Ejercicio1Luc%C3%ADa.assets/image-20240228021357079.png)

Gracias a este comando podemos comprobar que no se puede borrar `mariadb`, porque el contenedor `bbdd` está dependiendo de dicha imagen.s
