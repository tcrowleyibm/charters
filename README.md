# charters
A basic NodeJS application to manage charters data

# About
This application depends upon a back-end database. There are two endpoints associated with it:

 - `/dbtime` - makes a call the database to retrieve the time (`SELECT NOW()`). This endpoint doesn't
   require a table or any associated data
 - `/charters` - makes a call to the database to retrieve all charters defined within the `charters` table.


The application will attempt to read database credentials from the environment. It expects to find the
following environment variables:

```
 DB_USER
 DB_PW
 DB_HOST
 DB_NAME
 DB_PORT
```

For the `/charters` endpoint, it's necessary to create a table and add rows. This can be done several different
ways. To create the table and rows from the command line via psql, use the following:

```
psql -p 5432 -h localhost -U postgres -d postgres -f init.sql
```

# Running the application locally

Be sure to create an instance of Postgres and declare the credentials as environment variables. A
sample way to do this is:

```
export DB_USER="abetterusername"
export DB_PW="passwordie"
export DB_HOST="localhost"
export DB_NAME="postgres"
export DB_PORT="5432"
docker run --name postgres1 -e POSTGRES_PASSWORD=$DB_PW -e POSTGRES_USER=$DB_USER -p 5432:5432 -d postgres

```

To test access to the database:

```
psql -p 5432 -h localhost -U postgres
# use the password 'passw0rd' to authenticate
```

Install and start the application:

```
npm install
npm start
```

# Building the Docker image

```
docker build -t charters .
```

# Run the Docker image

```
docker run  --name charters1 --env DB_USER=abetterusername --env DB_PW=passwordie --env DB_HOST=host.docker.internal --env DB_NAME=postgres --env DB_PORT=5432 -p 3001:3001 -d charters:latest
```

# Running with SSL enabled

When running with SSL, use the following:

`export DB_USE_SSL=true`
