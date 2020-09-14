# DGraph-Example

This is a simple repository that demonstrates DGraph usage in golang

## Environment setup

You need to have [Go](https://golang.org/),
[Node.js](https://nodejs.org/),
[Docker](https://www.docker.com/), and
[Docker Compose](https://docs.docker.com/compose/)
(comes pre-installed with Docker on Mac and Windows)
installed on your computer.

Verify the tools by running the following commands:

```sh
go version
npm --version
docker --version
docker-compose --version
```

If you are using Windows you will also need
[gcc](https://gcc.gnu.org/). It comes installed
on Mac and almost all Linux distributions.

## Configure database

The default docker container runs in a self-sufficicent enviroment.
If you intend your databse to run in and independent environment
outside this docker container, modify the following files:

1. docker-compose.yml comment out the code that adds dgraph to
   the current environment and bundles it with the app
2. config.yml hold the dgraph config url. Modify the url
   according to your specific setup

## Start in development mode

In this configuration you have a total of 3 different
apps running in different ports

1. The dgraph server (zero, ratel, dgraph server are all bundled
   and being counted as one)
2. The golang backend, acting as the API endpoint
3. The Angular frontend, making requests to the API endpoint

In the project directory run the command (you might
need to prepend it with `sudo` depending on your setup):

```sh
docker-compose -f docker-compose-dev.yml up
```

This starts a local DGraph instance on http://localhost:8080`.
The database will be populated with test records
from the [init-db.js](init-db.js) file.

Navigate to the `server` folder and start the back end:

```sh
cd server
go run server.go
```

The back end will serve on http://localhost:3000.

Navigate to the `webapp` folder, install dependencies,
and start the front end development server by running:

```sh
cd webapp
npm install
npm start
```

The application will be available on http://localhost:3030.

## Start in production mode

In the project directory run the command (you might
need to prepend it with `sudo` depending on your setup):

Perform:

```sh
docker-compose up
```

This will build the application and start it together with
its database. Access the application on http://localhost:3000.

It also starts a local DGraph instance on http://localhost:8080`.
The database will be populated with test records
from the [init-db.js](init-db.js) file.
Production mode does not expose ratel

## Modification

This setup can easily be modified to separate frontend from
the backend.
Modify the [environment variable](webapp/src/environments/environment.ts)
and replace "apiUrl" with desired value