Suponemos que tienes instalado docker en el terminal.

Pon en el terminal la localización donde quieras construir el Dockerfile. Crea la imagen desde el Dockerfile:

```
sudo docker build -t shiny_image .
```
Con esto hemos creado dos imágenes: `shiny_image` y `rocker/shiny`. Vamos a correr `shiny_image` en un contenedor llamado `shiny_app`.

```
sudo docker run --name=shiny_app --rm -p 80:3838 shiny_image
```

Si vamos a [http://0.0.0.0/](http://0.0.0.0/) podremos ver la aplicación corriendo.
