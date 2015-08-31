## Magento - Odoo connector docker image 

This docker image is meant to be used for the development of https://github.com/OCA/connector-magento/

It:

* Installs Magento 1.7.0.2
* Installs the Magento Sample data
* Installs the PHP Magento module allowing to connect Odoo to Magento

### Requirements
This docker image expects 2 other linked containers to work .

1. Mysqldb or Mariadb linked as 'db'

2. Memcached linked as 'cache'

### Starting this container

```
$ docker run -td --name mariadb -e USER=user -e PASS=password  paintedfox/mariadb
```

```
$ docker run --name memcached -d -p 11211 sylvainlasnier/memcached
```

Build the image and run it
```
git clone https://github.com/guewen/docker-magento.git .
cd docker-magento
docker build -t docker-magento .
docker run -p 80:80 --link mariadb:db --link memcached:cache -td docker-magento 
```

The installation takes somes times as it needs to load the sample database.

Now visit your public IP in your browser and you will see the frontend.
The login/password for the backend is admin/admin25.


### Advanced information 

This Image will utilize the environment variables from the linked containers and automatically configure its magento itself.

Cache will be preconfigured.


### SSH 

Now as you think you may need to get into our Docker-magento container to be easily look into things, I did not package an SSH server just for this purpose.

You can use NSENTER to get into our container
#### https://github.com/jpetazzo/nsenter 


### Need support?

#### http://dockerteam.com

Credits:

Original image: https://github.com/paimpozhil/docker-magento

Please look at these repositories  for adding more parameters/configuring them 

#### https://github.com/SylvainLasnier/memcached/blob/master/README.md

#### https://github.com/Painted-Fox/docker-mariadb


