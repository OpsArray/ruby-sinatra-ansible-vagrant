# ruby-sinatra-ansible-vagrant
An automatically provisioned Vagrant box, using Ansible, that runs Ruby 2.2.3 and Sinatra 1.4.6

# Machine information
Operating System: Centos 7
Reverse Proxy Server: NGINX
Web Server: Unicorn
Ruby Version: 2.2.3
Sinatra Version: 1.4.6

# Developing an application
If you have a Sinatra project that you would like to start or continue working on, mount it to the vagrant box by using the environment variable APP_DIR

```
export APP_DIR=~/Projects/myproject/
```

Vagrant will mount this directory automatically to the location:

```
/var/www/html/production
```

Where Unicorn and NGINX knows to look for it.

# Using a backend database

[OpsArray](http://www.opsarray.com) has created a [MySQL Backend database Vagrant Box](https://github.com/OpsArray/mysql-ansible-vagrant) for use by any other vagrant boxes. Spin that up, and provision the tables and views that you need, and then point your web application to it via it's IP: 192.168.56.101.
