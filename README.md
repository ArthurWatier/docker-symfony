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
    
Install guide :
-

*Fork* the project on 

<https://github.com/ArthurWatier/docker-symfony> 

Clone it on ur machine
        
    `git clone https://github.com/YOUR-GIT-USERNAME/docker-symfony YOUR-PROJECT-NAME`
    
To build all the containers :

    cd YOUR-PROJECT-NAME
then build and run the containers

    docker-compose up -d

update composer symfony

    docker-compose run symfony composer update 
if you are in linux distro :
   give the good rights access for the var directory
    
        sudo setfacl -R -m u:www-data:rwX -m u:`whoami`:rwX symfony/var
        
   then
    
        sudo setfacl -dR -m u:www-data:rwX -m u:`whoami`:rwX symfony/var

   if this return error try to add the -n option
   
if u are on Mac distro or any distro who support the chmod +a option
   firt delete var and logs
        
        rm -rf var/cache/*
        rm -rf var/logs/*
        
   then set the rights for www-data
   
        sudo chmod -R +a "www-data allow delete,write,append,file_inherit,directory_inherit" symfony/var
   
   and 
   
        sudo chmod -R +a "`whoami` allow delete,write,append,file_inherit,directory_inherit" symfony/var

if u haven't changed exposed port to see the website go on 

    http://localhost:8000/

Typical errors when `docker-compose up -d` and how to fix
-

*Fix exposed ports troubles*
example error:
* ERROR: for *container-name*  
* Cannot start service postgres: driver failed programming external connectivity on endpoint *conitainer-name*
* Bind for 0.0.0.0:5432 failed: port is already allocated

Sometimes it's useful to force some services to be exposed on specific ports of the host machine, for example:
    
  * nginx couldn't be exposed on port 80 
  * postgresql couldn't be exposed on port 5432 
 
 1. In the root folder of the project copy the 
 
    `docker-compose.override.yml.dist`
    
 and name the copy   
    
    `docker-compose.override.yml`
 
 in the root folder of the project
 
 2. Rename the exposed ports of the services u want to change exposure
 
    example :
 ```yaml
 nginx:
  ports:
    - '3000:80'

 postgres:
  ports:
    - '5678:5432'
```
On ports expose the external port, the one you access the container by is always the left one the colon 
* (external:container)
* 3000:80 

will let you access for external connection by the url `localhost:3000/`

3. Force rebuild the containers with 


    docker-compose up -d --build

===================================================================

Start coding with your team and enjoy!

====================================================================