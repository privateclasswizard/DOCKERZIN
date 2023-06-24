FROM ubuntu:latest 
RUN apt-get update && apt-get -y upgrade 
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y git
RUN apt-get install -y apache2
RUN sed -i 's/#AddDefaultCharset ISO-8859-1/AddDefaultCharset ISO-8859-1/' /etc/apache2/apache2.conf
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y php libapache2-mod-php
RUN rm -rf /var/www/html/index.html
RUN echo "<?php phpinfo(); ?>" > /var/www/html/index.php
RUN ln -sf /etc/apache2/mods-available/php8.1.conf /etc/apache2/mods-enabled/php8.1.conf
RUN ln -sf /etc/apache2/mods-available/php8.1.load /etc/apache2/mods-enabled/php8.1.load
RUN rm -rf /var/www/html/index.html
RUN echo "<?php phpinfo(); ?>" > /var/www/html/index.php
RUN apt-get install -y postgresql
RUN apt-get install -y phppgadmin
RUN sed -i "s/$conf['extra_login_security'] = true;/$conf['extra_login_security'] = false;/g" /etc/phppgadmin/config.inc.php
WORKDIR /var/www/
COPY moodle-latest-402.tgz .
RUN tar xvfz /var/www/moodle-latest-402.tgz -C /var/www
RUN mkdir /var/moodledata
RUN chmod 777 /var/moodledata
RUN apache2ctl configtest
RUN apache2ctl graceful
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]