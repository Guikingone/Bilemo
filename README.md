# Bilemo 

The source code of the API project as asked in at OpenClassrooms in the DA PHP/Symfony path.

## Build

- Insight :

## Usage

Once you've installed Docker, time to build the project.

This project use Docker environment files in order to allow the configuration according to your needs,
this way, you NEED to define a .env file in order to launch the build.

**_In order to perform better, Docker can block your dependencies installation and return an error
or never change your php configuration, we recommand to delete all your images/containers
before building the project_**

```bash
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -a -q) -f
```

**Note that this command can take several minutes before ending**

Once this is done, let's build the project.

```bash
cp .env.dist .env
```

Update the informations linked to Docker then use Docker-Compose :

```bash
docker-composer up -d --build
```

Then you must use Composer in order to launch the application :

```bash
docker exec -it project_php-fpm sh

# Use Composer inside the container for better performances.
composer install
composer clear-cache
composer dump-autoload --optimize --classmap-authoritative --no-dev

# Configure BDD
./bin/console d:s:c # for classic users

# Fixtures
./bin/console d:f:l -n
```

Once this is done, access the project via your browser :

- Dev :

```
http://localhost:port/
```

**For the production approach, you must update the .env file and change the APP_ENV and APP_DEBUG keys.**

- Prod :

```
http://localhost:port/
```

If you need to perform some tasks:

```bash
docker exec -it project_php-fpm sh
```

Once in the container:

```bash
# Example for clearing the cache
./bin/console c:c --env=prod || rm -rf var/cache/*
```

**Please note that you MUST open a second terminal in order to keep git ou other commands line outside of Docker**

### PHP CLI

```bash
cd core
php bin/console s:r || ./bin/console s:r || make serve
```

Then access the project via your browser:

```
http://localhost:8000
```

**The commands listed before stay available and needed for this approach**

## Contributing 

This project isn't open for contribution, please use the Issues/Pull Request panels.
