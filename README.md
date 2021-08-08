# Jinaga Images

Docker images for use with [Jinaga](https://jinaga.com)

## jinaga-postgres-fact-keystore

A PostgreSQL database with the Jinaga fact and keystore schemas already installed.

To use, set the following environment variables:

| Environment Variable | Description                           |
| -------------------- | ------------------------------------- |
| POSTGRES_PASSWORD    | Password for "postgres" admin account |
| APP_USERNAME         | Username for the application account  |
| APP_PASSWORD         | Password for the application account  |
| APP_DATABASE         | Name of the application database      |

Expose port 5432 so that applications can connect to PostgreSQL.

For example:

```bash
docker run --name jinaga-postgres -p5432:5432 -e POSTGRES_PASSWORD=secretpw -e APP_USERNAME=appuser -e APP_PASSWORD=apppw -e APP_DATABASE=appdb jinaga/jinaga-postgres-fact-keystore
```

You can then connect with the command line:

```bash
psql -h localhost -U appuser appdb
```

And enter the password `apppw`.

Or use the connection string:

```
postgresql://appuser:apppw@localhost:5432/appdb
```

To build:

```bash
cd jinaga-postgres-fact-keystore
docker build -t jinaga/jinaga-postgres-fact-keystore .
```

This image is based on the official [postgres](https://hub.docker.com/_/postgres) image.