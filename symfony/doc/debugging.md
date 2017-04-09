# Remote debugging with Xdebug in PHPStorm with Docker container

Inspired from tutorials that can be found [here](https://gist.github.com/chadrien/c90927ec2d160ffea9c4) and [here](https://gist.github.com/jehaby/61a89b15571b4bceee2417106e80240d).

## Update the `docker-compose` configuration
Some configuration should be added to your personal `docker-composer.override.yml`:
```yaml
  symfony:
    environment:
    XDEBUG_CONFIG: 'remote_host={{YOUR_IP_ADDRESS}} idekey={{XDEBUG_IDE_KEY}}'
    PHP_IDE_CONFIG: 'serverName={{PHPSTORM_SERVER_NAME}}'
```
Don't forget to replace the placeholders with the proper value:
 - **YOUR_IP_ADDRESS**: the current IP address of the host machine on the network (check it with `ifconfig`);
 - **XDEBUG_IDE_KEY**: Default for PHPStorm is `PHPSTORM` but if you customized it in PHPStorm replace it with the proper value;
 - **PHPSTORM_SERVER_NAME**: The name of your local server as configured in PHPStorm (see below for further information).

Then run `docker-compose up -d` to take this new configuration into account.

## Configure PHPStorm to enable remote debugging with Xdebug

### Configure the Debug Proxy
Configure the `Languages & Frameworks > PHP > Debug > DBGp Proxy` section of the PHPStorm configuration and define the following parameters:
![][xdebug-dbgp-proxy]

### Configure the server and the path mapping
Click on the empty selection field in the top right corner of your PHPStorm IDE and select "Edit configurations":
![][xdebug-configuration-start]

Then click on "+" and select "PHP Remote Debug":
![][xdebug-remote-debug]

Fill in the name of the configuration and click on the "..." button next to the "Servers" field to create a new server configuration:
![][xdebug-remote-configuration]

And configure the new server as follows (assuming your local server can be found on `listo.local` for example). Mind the path mapping setting on the directories:
![][xdebug-server-configuration]

Once the server created you should have the following configuration:
![][xdebug_remote_final]

If you validate your configuration you will be able now to enable debugging by clicking on the top right green bug. Your debugging section should then display like this:
![][xdebug-enabled]

    [xdebug-configuration-start]: images/xdebug_configuration_start.png
[xdebug-dbgp-proxy]: images/xdebug_dbgpproxy.png
[xdebug-enabled]: images/xdebug_enabled.png
[xdebug-remote-configuration]: images/xdebug_remote_configuration.png
[xdebug-remote-debug]: images/xdebug_remote_debug.png
[xdebug-remote-final]: images/xdebug_remote_final.png
[xdebug-server-configuration]: images/xdebug_server_configuration.png
