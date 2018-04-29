**Docker WordPress**

This Docker configuration install all you need for a functional wordpress site (Apache, PHP, MysqL, PHPMyadmin, Wordpress latest)

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
- Docker Start : docker-compose up -d

 - The localhost will be available at: localhost:8080 (port can be changed in docker-compose.yml)
 - The wordpress site : localhost:3000 (port can be changed in docker-compose.yml)
 - PHPMyadmin : localhost:8081 (port can be changed in docker-compose.yml)

- Usefuls Docker commands: 
 - docker-compose up/down (Start/Stop docker env)
 - docker-compose rm -v (remove all running docker)
 - docker-compose ps (list all running docker)
