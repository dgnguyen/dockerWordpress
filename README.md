Docker WordPress

1- Useful links :
 - https://lindev.fr/index.php?post/2017/06/06/Environnement-de-d%C3%A9veloppement-complet-avec-Docker
 - https://medium.com/cluetip/wordpress-development-made-easy-440b564185f2
 - https://medium.com/@tatemz/local-wordpress-development-with-docker-3-easy-steps-a7c375366b9

2- Step by step :
- Create new wordpress site folder in www/
- Add wordpress image in /docker-compose.yml :
```
###########################
# Setup the Wordpress container
###########################
    wordpress:
        container_name: dockerapache_wordpress
        image: wordpress:latest
        ports:
            - 3000:80
        environment:
            - WORDPRESS_DB_HOST=mysql
            - WORDPRESS_DB_USER=project
            - WORDPRESS_DB_PASSWORD=project
            - WORDPRESS_DB_NAME=project
        volumes:
            - ./www/wordpress:/var/www/html
            - ./www/wordpress/wp-content:/var/www/html/wp-content
        links:
            - mysql:mysql
###########################
```
- Create new Apache configuration of new wordpress site in /apache/vhosts/wordpress.conf
- Start Docker : docker-compose up -d
