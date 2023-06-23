FROM ubuntu:latest 
# Atualizar o sistema
RUN apt-get update && apt-get -y upgrade 
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y git

# Instalar o Apache2
RUN apt-get install -y apache2
# Editar o arquivo apache2.conf
RUN sed -i 's/#AddDefaultCharset ISO-8859-1/AddDefaultCharset ISO-8859-1/' /etc/apache2/apache2.conf

# Instalar o PHP5 e o módulo do Apache
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y php libapache2-mod-php

# Criar arquivo PHP de teste
RUN rm -rf /var/www/html/index.html
RUN echo "<?php phpinfo(); ?>" > /var/www/html/index.php
# Habilitar módulo PHP5 no Apache
RUN ln -sf /etc/apache2/mods-available/php8.1.conf /etc/apache2/mods-enabled/php8.1.conf
RUN ln -sf /etc/apache2/mods-available/php8.1.load /etc/apache2/mods-enabled/php8.1.load
# Instalar o MySQL
RUN apt-get install -y mysql-server

# Instalar o phpMyAdmin
RUN apt-get install -y php-mysql
RUN apt-get install -y phpmyadmin

# copiando o Moodle para o diretório /var/www
WORKDIR /var/www/
COPY moodle-latest-402.tgz .
RUN tar xvfz /var/www/moodle-latest-402.tgz -C /var/www
# Criar diretório moodledata e definir permissões
RUN mkdir /var/moodledata
RUN chmod 777 /var/moodledata

EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]