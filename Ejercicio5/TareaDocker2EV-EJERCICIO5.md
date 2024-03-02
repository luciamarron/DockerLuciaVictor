# EJERCICIO 5 
*Arranca un contenedor que ejecute una instancia de la imagen php:7.4-apache , que se llame web
y que sea accesible desde un navegador en el puerto 8000.*
- Tenemos que hacer pull a la imagen de `php:7.4 apache`.

```bash
sudo docker pull php:7.4-apache
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/dd24fa95-bc66-4033-b271-6fadaae94f3c)

- Luego lo arrancamos con el nombre web en el puerto 8000.
```bash
docker run -d -p 8000:80 --name web php:7.4-apache
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/053b8776-146b-479e-b566-5031be411c6c)

*Coloca en el directorio raíz del servicio web ( /var/www/html ) un sitio web donde figure el nombre
de los componentes del grupo - el sitio deberá tener al menos un archivo index.html y un archivo
.css*
```bash
docker cp index.html  web:/var/www/html
docker cp estilos.css  web:/var/www/html
docker cp mes.php  web:/var/www/html
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/cda31351-42a5-46bc-bc7c-18bb605e3e69)

- *Sitio web donde figure el nombre de los componentes del grupo*

![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/c13cd8ad-f324-4b75-8659-c5af06d9bd49)

- *Coloca en ese mismo directorio raíz un archivo llamado mes.php que muestre el nombre del mes actual.Ver la salida del script en el navegador*

![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/7a08b2e9-eea2-4371-b1f3-2c7fd75ae43b)

*Borra el contenedor*
```bash
docker stop web
docker rm web
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/c622f18c-bd6c-41f2-a614-ade1f5369160)

*Automatiza estas operaciones creando un fichero de Dockerfile*

``` bash
 ## Archivo DockerFile ##

# Especificamos la imagen que queremos hacer el pull.
FROM php:7.4-apache
# Le decimos que coja los archivos que hay en la carpeta en la que se encuentra en el dockerfile y los copie a var/www/html
COPY . /var/www/html/
# Exponemos el puerto 8000 para que sea accesible desde el exterior
EXPOSE 8000
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/46ef47bd-a58f-471c-9b91-3bee9ca7d1cc)
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/d2d3a2de-0d96-45e8-9fba-771552d24088)

*Desde la carpeta `html` ejecutamos los siguientes comandos*
```bash
#Buildeamos el archivo dockerfile con el nombre de imagen victorlucia/ejercicio5
docker build -t victorlucia/ejercicio5 .
# ejecutamos la imagen en el puerto 8000 como daemon con el nombre web
docker run -d -p 8000:80 --name web victorlucia/ejercicio5
```
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/b8a66a30-8d93-4654-ac1e-5e0c7dea7bfb)
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/843e2373-7676-4d91-b841-a141fc560713)
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/65df1f7c-1b1b-4943-ab80-718ed1d95b93)

*Push de la imagen a dockerhub*
```bash
## Iniciamos sesion en dockerhub
docker login
## Le ponemos una tag a la imagen con tu nombre de usuario (tuve que cambiar el nombre porque era muy lioso el otro que habia puesto pero es lo mismo)
docker tag ejercicio5:v1 victor9/ejercicio5:v1
## Hacemos el Push de la imagen 
docker push victor9/ejercicio5:v1
```
*Push desde terminal*
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/5831fbc8-4f88-47b7-8666-352fef7d35ab)
*Imagen en Dockerhub: https://hub.docker.com/r/victor9/ejercicio5/tags*
![imagen](https://github.com/luciamarron/DockerLuciaVictor/assets/100193393/84f0e8e9-e8ad-4611-bfe4-1c8756bf466c)
