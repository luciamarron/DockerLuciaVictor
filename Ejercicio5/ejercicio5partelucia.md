# Ejercicio 5 Parte Lucía
Primero hago un pull del ejercicio 5 de la parte de Víctor
```bash
sudo docker pull victor9/ejercicio5:v1
```
![Captura de pantalla 2024-03-03 204710](https://github.com/luciamarron/DockerLuciaVictor/assets/92050490/e73fdd59-c883-4576-ba60-d5e86ce05fd7)

Seguidamente creamos el nuevo contenedor al que llamaremos 'weblucia'
```bash
sudo docker run -d -p 8000:80 --name weblucia victor9/ejercicio5:v1
```
![Captura de pantalla 2024-03-03 205753](https://github.com/luciamarron/DockerLuciaVictor/assets/92050490/06f64a16-5d30-473a-843d-5cdee8e14575)

## Visualización del sitio web en el puerto 8000
![Captura de pantalla 2024-03-03 210233](https://github.com/luciamarron/DockerLuciaVictor/assets/92050490/a0f6153d-daed-4dc7-bbc6-eb35dc3fb776)

## Visualización fichero mes.php en el puerto 8000
![Captura de pantalla 2024-03-03 210304](https://github.com/luciamarron/DockerLuciaVictor/assets/92050490/5a63f0b5-e783-45af-a153-d6ad19296a90)
