# Running the Todo List with Docker Compose

## Prerequisites

- Docker Desktop (or Docker Engine) with the Docker Compose plugin.
- Port `8000` available on your machine. MySQL is reachable by the application on the private Compose network and is not published to the host.

## Start the application

Open a terminal in the directory containing `docker-compose.yml`, then run:

```sh
docker compose up --build
```

Compose builds the Django and MySQL images, starts MySQL, waits for its health check, and then starts the application. The application runs Django migrations before starting the web server. Visit [http://localhost:8000](http://localhost:8000).

To run the containers in the background instead, use:

```sh
docker compose up --build -d
```

View application and database logs with:

```sh
docker compose logs -f
```

## Stop the application

Stop and remove the containers and Compose network while retaining the database volume:

```sh
docker compose down
```

To stop the background containers without removing them, run:

```sh
docker compose stop
```

The named `mysql_data` volume preserves todos and other database data across container stops, removals, and rebuilds. To permanently delete the containers and database data, run:

```sh
docker compose down --volumes
```

Set `MYSQL_PASSWORD` and `MYSQL_ROOT_PASSWORD` in the shell environment before starting Compose to override the local development defaults. If the database volume already exists, MySQL keeps the credentials and database initialized in that volume; changing the environment values alone does not change its existing accounts.