# Django REST Framework Tutorial
> Source: [Django Rest Framework Quickstart](https://www.django-rest-framework.org/tutorial/quickstart/)

## Setup
- Install `docker` and `docker-compose`.
- Launch the servers:
  ```bash
  docker compose up
  ```
  This command will also build a custom apache django docker image.
  > Note: The django web server will listen to port `8000`. 
- Additionally run a local development server on your current os:  
  Add the following line to `/etc/hosts`:  
  ```hosts
  127.0.0.1   db
  ```
  Run the server and it will connect automatically to docker container.

  ```bash
  python manage.py runserver 0:8001
  ```
  > This server will listen to port 8001

- To connect to the local database server:  
  * Add the following to `~/.pg_service.conf` file:  
    ```conf
    [djangodb]
    host=localhost
    port=5432
    dbname=djangodb
    user=dbuser
    password=dbpassword
    ```
  * Connect to the server:  
    ```bash
    psql service=djangodb
    ```

- After the database instance is run, connect to the database and create a database named `djangodb` 
  ```sql
  CREATE DATABASE djangodb;
  ```
- Make migratiosn to the database.
  ```bash
  python manage.py makemigrations polls
  ```

- Migrate changes to the database.
  ```bash
  python manage.py Migrate
  ```
- Restart docker compose.

- Populate the database with some data:  
  Run `python manage.py shell` and run the contents of the file `init/part-2_populate-database.py` in the shell.(Part 2)

- Create superuser:  
  ```bash
  python manage.py createsuperuser
  ```
  Username: admin  
  Email address: admin@example.com
  Password: pass


## Tips
- View the SQL output of a migration:  
  ```bash
  python manage.py sqlmigrate polls 0001
  ```

- Drop into django shell
  ```bash
  python manage.py shell
  ```

