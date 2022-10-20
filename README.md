# [Backstage](https://backstage.io)

This is your newly scaffolded Backstage App, Good Luck!

Use below commands to build docker image for the application from root directory.

```shell
podman image build . -f packages/backend/Dockerfile --tag backstage-sample-app
podman image tag localhost/backstage-sample-app:latest quay.io/lrangine/backstage-sample-app:1.0
podman image push quay.io/lrangine/backstage-sample-app:1.0
```

Use below commands to run the application using docker image. This docker image is expected to connect to postgres database running on another database in the same host. 

```shell
# run postgres database
podman run --name myPostgresDb -p 5432:5432 -e POSTGRES_USER=postgresUser -e POSTGRES_PASSWORD=postgresPW postgres
# run the backstage application connecting to postgres database.
podman run -it -p 7007:7007 -e POSTGRES_USER=postgresUser -e POSTGRES_PASSWORD=postgresPW -e POSTGRES_SERVICE_HOST=192.168.0.140 -e POSTGRES_SERVICE_PORT=5432 quay.io/lrangine/backstage-sample-app:1.0
```
