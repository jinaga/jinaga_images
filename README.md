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

## jinaga-replicator

The Jinaga Replicator is a single machine in a network.
It stores and shares facts.
To get started, create a Replicator of your very own using [Docker](https://www.docker.com/products/docker-desktop/).

```
docker pull jinaga/jinaga-replicator
docker run --name my-replicator -p8080:8080 jinaga/jinaga-replicator
```

This creates and starts a new container called `my-replicator`.
The container is listening at port 8080 for commands.
Use a tool like [Postman](https://www.postman.com/) to `POST` messages to `http://localhost:8080/jinaga/write` and `/read`.
Or configure a Jinaga client to connect to the Replicator.

```typescript
import { JinagaBrowser } from "jinaga";

export const j = JinagaBrowser.create({
    httpEndpoint: "http://localhost:8080/jinaga"
});
```