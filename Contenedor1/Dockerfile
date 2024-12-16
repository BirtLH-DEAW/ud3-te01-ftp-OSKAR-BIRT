# crear la imagen
# Utilizamos la imagen base de Ubuntu
FROM ubuntu:latest

# Actualizamos el sistema de paquetes y los repositorios e
# instalamos el editor nano y proftpd
RUN apt-get update \
   && apt-get install -y nano \
   && apt-get install -y proftpd

# Copiamos nuestros archivos al contenedor creando las carpetas
# RUN mkdir /var/www/html/default_website \
COPY /contenido /srv/ftp/
COPY proftpd.conf /etc/proftpd/proftpd.conf

# Exponemos el puerto 21 para la conexión y el rango del 50000 al 50030 para los datos
EXPOSE 21
EXPOSE 50000:50030

# Comando por defecto para iniciar el contenedor
#CMD ["service", "proftpd", "start"]