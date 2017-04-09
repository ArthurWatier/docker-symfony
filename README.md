Ready to use docker + symfony
=======

commands:

    docker-compose up -d
then go on 

    http://localhost/

to see the website
if var dir isn't writable check     
most of linux dist will have to do:

    sudo setfacl -R -m u:"$HTTPDUSER":rwX -m u:`whoami`:rwX symfony/var
else go to :

    http://symfony.com/doc/current/setup/file_permissions.html
and follow the steps until u can reload localhost and see the project working,
