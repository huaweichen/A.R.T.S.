---
layout: default
title:  "PHP xDebug Theory and Setup"
permalink: php-xdebug-theory-and-setup.html
---

### PHP xDebug Theory and Setup

[PHP xDebug with Docker](https://www.huaweichen.com/2019/php-xdebug-with-docker/)

##### The Story
On Friday, we had a Dockerized system, not Vagrant + VirtualBox anymore. It is a great improvement. But the xDebug for our PHP apps are broken.
Previously, our setup was ONE single PHP in Vagrant. And if we need to run PHP 5.6, we switch to 5.6, if we need 7.2, we switch to 7.2. 
Now in Docker, our DevOps guys, build every PHP app image, based on PHP image. So in `docker-compose.yaml` file, it is not app1 `links` to PHP5 or `depends_on` PHP5, it is a solid image. Good or bad will discuss in future.
 
##### The Problem

I can not click in browser, then debug my frontend app, as well as backend app anymore. Because the PHP in Intellij can only either frontend PHP or backend PHP. When I debug `$this->postRequest($backendURL, $frontEndData);` in frontend app, it does not go to backend code anymore, it remains in frontend code, and skip to the next line.

##### The Solution 

Create two separate project in Intellij. Launch them separately, so that one is listen to frontend PHP and the other listen to backend PHP. 

##### How It Works 

1. Create two projects separately in Intellij, one is Frontend, one is Backend.

1. Setup each project's 
    1. PHP CLI (from Docker)
    1. Server: server name, host and file mapping.
    1. Debug: 
        1. Frontend: port 9001, ide_key="CLIENT"
        1. Frontend: port 9002, ide_key="SERVER"
1. Setup xdebug.ini in Docker scripts.
    1. Frontend:
    ```editorconfig
         # ... other code 
         xdebug.remote_enable=1
         xdebug.remote_host=192.168.20.68 ;My PC's IP
         xdebug.remote_port=9001 ;Two projects using different port.
         xdebug.remote_autostart=1 ;Auto start for every connection
         xdebug.idekey=CLIENT ;But in Intellij, I set up ignore and filter out by IDE Key.
         xdebug.remote_connect_back=0 ;I explicitly turn this off, because I specify the host.
         ;xdebug.remote_handler=”dbgp” ;I comment this out, I don't think in same PC connect to same IP address, need DBGp plugin.
         # ... other code
    ```
    1. Backend:
    ```editorconfig
         # ... other code
         xdebug.remote_enable=1
         xdebug.remote_host=192.168.20.68 ;My PC's IP
         xdebug.remote_port=9002 ;Two projects using different port.
         xdebug.remote_autostart=1 ;Auto start for every connection
         xdebug.idekey=SERVER ;But in Intellij, I set up ignore and filter out by IDE Key.
         xdebug.remote_connect_back=0 ;I explicitly turn this off, because I specify the host.
         ;xdebug.remote_handler=”dbgp” ;I comment this out, I don't think in same PC connect to same IP address, need DBGp plugin.
         # ... other code
    ```
1. Also I helped colleague to setup his xDebug in Symfony CLI.
    1. Turn on the port in Windows docker machine

    1. Run this in CLI. So that XDEBUG config are exported.
    ```editorconfig
    export XDEBUG_CONFIG="remote_enable=1 remote_mode=req remote_port=9001 remote_host=192.168.20.68 remote_connect_back=0"
    ```
    
    1. Run this in CLI. So that IDE config are exported.
    ```editorconfig
    export PHP_IDE_CONFIG="serverName=Frontend" # it's the server name in `servers` list.
    ```

    1. Map folder structures.
    
1. Wrote a confluence page for the team.
