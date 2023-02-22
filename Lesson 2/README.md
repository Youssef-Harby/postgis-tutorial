# Lesson 2

## To install PostgreSQL and PostGIS using Docker Compose, you can follow the steps below:

 1. Install Docker and Docker Compose on your system. You can find installation instructions for your operating system on the Docker website.
   - https://www.youtube.com/watch?v=fnjs4W91Olc
   - https://www.youtube.com/watch?v=oGbEqWG-7LQ
   - https://docs.docker.com/engine/install/

 2. Create a new directory for your Docker Compose project and navigate into it:

    ```bash
    mkdir my_postgis_project
    cd my_postgis_project
    ```
 3. Create a new file called docker-compose.yml in this directory and open it in a text editor:
  
    ```bash
    touch docker-compose.yml
    nano docker-compose.yml
    ```
    ```yaml
    version: '3.8'  # specify the version of docker-compose syntax to use

    services:
    postgis:  # define a service for the PostGIS container
        image: postgis/postgis:15-3.3-alpine  # use the PostGIS image from Docker Hub
        container_name: postgis  # specify the name of the container
        environment:  # set environment variables for the container
        POSTGRES_PASSWORD: mysecretpassword  # set the password for the default Postgres user
        POSTGRES_DB: tutorial # default database to create on the first startup
        volumes:  # mount a volume to persist the Postgres data
        - pgdata:/var/lib/postgresql/data
        ports:  # expose the container's port for incoming connections
        - "25432:5432"
        networks:  # connect the container to a named network
        - app-network

    pgadmin:  # define a service for the PgAdmin container
        image: dpage/pgadmin4:6.20  # use the PgAdmin image from Docker Hub
        container_name: pgadmin4  # specify the name of the container
        environment:  # set environment variables for the container
        PGADMIN_DEFAULT_EMAIL: admin@example.com  # set the email for the default PgAdmin user
        PGADMIN_DEFAULT_PASSWORD: mysecretpassword  # set the password for the default PgAdmin user
        volumes:  # mount a volume to persist the PgAdmin data
        - pgadmindata:/var/lib/pgadmin
        ports:  # expose the container's port for incoming connections
        - "5050:80"
        depends_on:  # specify that the PgAdmin container depends on the PostGIS container
        - postgis
        links:  # create a network link between the PgAdmin and PostGIS containers
        - postgis
        networks:  # connect the container to a named network
        - app-network

    networks:
    app-network:  # define a named bridge network for the containers to connect to
        driver: bridge

    volumes:
    pgdata:  # define a named volume for the Postgres data
    pgadmindata:  # define a named volume for the PgAdmin data
    ```
    ctrl+x then y and enter to save

1. start the services with Docker Compose:

   This command will start the services defined in the docker-compose.yml file, create the database and enable the PostGIS extension, and expose the necessary ports for accessing the services.

   ```bash
   docker compose up -d
   ```
2. Once the container is running, open a new terminal window and use the docker ps command to get the container ID:

    This command will list all running Docker containers and their IDs. Look for the container with the postgis image and note/copy its ID.
    ```bash
    docker ps
    ```
3. Use the docker exec command to run a psql command inside the container:
4. 
    Replace <container_id> with the container ID you noted in step 2, and <database_name> with the name of the PostgreSQL database you want to connect to. You will be prompted to enter the password for the postgres user.

     - Once you are connected to the database, you can run SQL queries using the psql command prompt.

     - When you are finished, you can exit the psql command prompt by typing \q, and then exit the Docker container by typing exit.

    That's it! You have now run a psql command inside the PostGIS Docker container using the docker exec command.

    ```bash
    docker exec -it <container_id> psql -U postgres -d <database_name>
    ```