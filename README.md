# docker.django
Use docker to develop and test django framework

I follow this url steps.
https://docs.docker.com/compose/django/

This is a quick start to develop using this framework

We have 3 basic files
- Dockerfile
	Used to build a new image starting from Python3
	And install django (defined on requirements.txt)
- requirements.txt
	Define the required software to install
	- Django: Our framework
	- psycopg2: Postgres adapter for python
- docker-compose.yml
	Call to build our image, and after the build run the server
	Also pull and start the postgres image

This this 3 files you need run docker-compose command 
```
sudo docker-compose run web django-admin startproject composeexample .
```

This command going to build the image web, but the container is used to create the example

With the container web the next instruction said to django-admin i need to start a new project
called composeexample in this '.' path (To develop other proyect change the name use your ount proyect cool name)

When django-admin ends the container is killed, but the container is using this path to construct.
So the folder composeexample was created, and we going to modify the settings.py to conect django with
postgres

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

So finally we run our containers with
```
docker-compose up
```
The output should display the port in our machine to check the instalation
```
 docker-compose up
djangosample_db_1 is up-to-date
Creating djangosample_web_1 ...
Creating djangosample_web_1 ... done
Attaching to djangosample_db_1, djangosample_web_1
db_1   | The files belonging to this database system will be owned by user "postgres".
db_1   | This user must also own the server process.
db_1   |
db_1   | The database cluster will be initialized with locale "en_US.utf8".
db_1   | The default database encoding has accordingly been set to "UTF8".
db_1   | The default text search configuration will be set to "english".

. . .

web_1  | May 30, 2017 - 21:44:49
web_1  | Django version 1.11.1, using settings 'composeexample.settings'
web_1  | Starting development server at http://0.0.0.0:8000/
web_1  | Quit the server with CONTROL-C.
```

If you don't want to keep your command line bussy use:
```
docker-compose up -d
```

And you can stop the containers using
```
docker-compose down
```

