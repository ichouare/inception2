
FROM debian:bullseye


RUN apt-get update -y && apt-get upgrade -y
RUN  apt-get install  wget -y 
RUN apt-get install -y php7.3\
	php-fpm\
	php-mysql\
	php-curl\
	php-gd\
	php-intl\
	php-mbstring\
	php-soap\
	php-xml\
	php-xmlrpc\
	php-zip\
	mariadb-client\
	php-redis\
	curl
	
COPY  ./conf/wp-config.php /
RUN wget  https://wordpress.org/latest.tar.gz  -P /var/www/
RUN cd /var/www && tar xzvf latest.tar.gz && chown -R root:root /var/www/wordpress
RUN cp /var/www/wordpress/wp-config-sample.php  /var/www/wordpress/wp-config.php
COPY ./tools/script.sh /script.sh
RUN chmod +x script.sh
RUN sed -i 's/listen = \/run\/php\/php7.4-fpm.sock/listen = 0.0.0.0:9000/g' /etc/php/7.4/fpm/pool.d/www.conf
RUN service php7.4-fpm start
RUN mkdir -p /run/php
CMD ["./script.sh"]
