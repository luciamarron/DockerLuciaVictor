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

Accedemos a la aplicación HTML desde el navegador visitando http://localhost:8080

![image-20240223100755769](Ejercicio1Luc%C3%ADa.assets/image-20240223100755769.png)

### 1.2. Arrancar un contenedor que se llame bbdd y que ejecute una instancia de la imagen mariadb para que sea accesible desde el puerto 3306.



### 1.3. Establecer las variables de entorno necesarias.

·La contraseña de root sea root . 

·Crear una base de datos automáticamente al arrancar que se llame prueba . 

·Crear el usuario invitado con la contraseña invitado .



