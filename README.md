# OpenCart Docker

This repository should make it simple to run [Opencart](http://www.opencart.com/) in docker containers.

## Installation

1.  Firstly, clone or download the opencart project.

        If you are getting from Git then don't get from the master branch.. It may be unstable... Select a branch that is currently stable. The below branch worked for me however it may already be outdated by the time you read this.

        $ git clone -b 3.0.2.1_rc https://github.com/opencart/opencart.git my-opencart

2.  Clone the opencart-docker project as a sub module.

        $ cd my-opencart
        $ git submodule add https://github.com/numberformat/opencart-docker.git

3.  It should look a bit like this:

        |-- my-opencart
        |   |-- opencart-docker
        |   |-- tests
        |   |-- upload
        |   |-- vendor
        |   |-- build.xml
        |   |-- changelog.md
        |   |-- etc...

4.  IMPORTANT! Customize the `.env` file and make any changes to the environment variables that you want.

        $ vi opencart-docker/.env

5.  Now, in the opencart-docker folder, we want run it and serve Opencart. The simplest way is:

    $ cd opencart-docker
    $ docker-compose up -d apache mysql

6.  Confirm all 3 containers are up

        $ docker ps

7.  Finally we need to be able to access the site. This will be different on different operating systems. The following are just 2 example implementations

### Linux

1.  Simple. Docker is native so open `/etc/hosts` and add

        127.0.0.1 opencart.dev

### If your using Windows with Docker CE

1.  Firstly, make sure the docker-machine is up and running and type the command `docker-machine ip`
2.  Copy this value, usually `192.168.99.100`
3.  Add this to your HOSTS file (usually) `C:/Windows/System32/drivers/etc/hosts`

        192.168.99.100 opencart.dev

4.  Visit http://opencart.dev/

### If your using Virtualbox on Windows running Linux

1. Open your Virtual machine Settings -> Network -> Adapter 1
2. Change Attached to: NAT
3. Go to Advanced -> Port Forwarding Add the following
   - Name: HTTP
   - Host Port: 80
   - Guest port: 80
   - Leave other fields blank
4. Create an empty `config.php` file in both `upload/` and `upload/admin/`.
5. Verify your docker continer is running as a user that has read/write permissions to the folders. For example you will need to do the following in order for your container to have access. This step depends on your OS so your mileage will vary.

```sh
chown -R www-data:www-data to the ../upload folder
```

#### Configure Opencart

1.  Visit http://localhost

2.  Click continue you will be presented with a multi-step setup process. In the pre-installation step make sure everything is green. In the config step enter the values from your .env file. The defaults are:

        - **hostname**: mysql
        - **username**: opencart
        - **password**: password
        - **database**: opencart

3.  You will get a message to move your storage directory. You can close this message out and move the directory when you get a chance.

## Notes

If you make changes to this project you may need to rebuild the images.

`docker-compose build`

### Remove all images and containers

- `docker rm -f $(docker ps -a -q)` - removes all containers
- `docker images -q | cut -f1 -d' ' | xargs docker rmi` - removes all images
