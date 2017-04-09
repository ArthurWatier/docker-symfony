Ready to use symfony ngnix postgres
=

Requirements :
-
1. Intall _Docker_ for your _distro_ :
    * Docker for _Mac_ : 
        <https://docs.docker.com/docker-for-mac/install/>
    * Docker for _Windows_ :
        <https://docs.docker.com/docker-for-windows/install/>
    * Docker for _Linux Ubuntu_ :
        <https://docs.docker.com/engine/installation/linux/ubuntu/>
    * Docker for _Debian_ : 
        <https://docs.docker.com/engine/installation/linux/debian/>
       
2. Install _docker-compose_ :
    * <https://docs.docker.com/compose/install/>
    
How to install in 3 commands :
-
To build all the containers :

    docker-compose up -d
    
    docker-compose run symfony composer update 
    
    docker-compose run symfony mkdir var 
    
    docker-compose run symfony chown -R www-data:www-data var

to see the website go on 

    http://localhost:8000/







Typical errors when `docker-compose up -d` and how to fix
-
example :
* ERROR: for *container-name*  
* Cannot start service postgres: driver failed programming external connectivity on endpoint *conitainer-name*
* Bind for 0.0.0.0:5432 failed: port is already allocated

Sometimes it's useful to force some services to be exposed on specific ports of the host machine, for example:
    
  * nginx couldn't be exposed on port 80 
  * postgresql couldn't be exposed on port 5432 
 
 1. To do so, copy the `docker-compose.override.yml.dist` as `docker-compose.override.yml` in the root folder of the project
 2. Here is an example of how to expose other ports :
 ```yaml
 nginx:
  ports:
    - '3000:80'

 postgres:
  ports:
    - '5678:5432'
```
On ports expose the external port (the one you need to access the container) is always the left one the colon 
* (external:internal)
* '3000:80'
    
will let you access for external connection by the url `localhost:3000/` 