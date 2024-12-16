# crear la imagen
# Utilizamos la imagen base de Ubuntu
FROM ubuntu:latest

# Actualizamos el sistema de paquetes y los repositorios e
# instalamos el editor nano y proftpd
RUN apt-get update \
   && apt-get install -y nano \
   && apt-get install openssl \
   && apt-get install -y proftpd \
   && apt-get install -y proftpd-mod-crypto

# Creamos el usuario deaw con password deaw
RUN useradd -m -d /srv/deaw -s /sbin/nologin deaw
RUN echo "deaw:deaw" | chpasswd

# Copiamos nuestros archivos al contenedor creando las carpetas
# RUN mkdir /var/www/html/default_website \
COPY /contenido /srv/deaw/
COPY proftpd.conf /etc/proftpd/proftpd.conf
COPY tls.conf /etc/proftpd/tls.conf
COPY modules.conf /etc/proftpd/modules.conf
COPY certs/proftpd.pem /etc/ssl/certs/proftpd.pem
COPY certs/proftpd.key /etc/ssl/private/proftpd.key
RUN chmod 640 /etc/ssl/certs/proftpd.pem
RUN chmod 640 /etc/ssl/private/proftpd.key

# Exponemos el puerto 21 para la conexión y el rango del 50000 al 50030 para los datos
EXPOSE 21
EXPOSE 50000:50030

# Comando por defecto para iniciar el contenedor
#CMD ["service", "proftpd", "start"]