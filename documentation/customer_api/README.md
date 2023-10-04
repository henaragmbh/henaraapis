# Customer API

This API provides and encapsulates access to the *Customer* data persisted in internal databases, one for each *Praxis Group*.

Users of this API can manage their data via this API to combine Henara services with their own applications.


## Test System

You can test the API with a self hosted test system which is based on the [docker compose](https://docs.docker.com/compose) technology.

So you need a docker host. Among various methods you could install [Docker Desktop](https://www.docker.com/products/docker-desktop) to run a docker host on your desktop machine.

With the files *docker-compose.yml* and *config.env* (provided in this folder), and *config.env* updated to your needs, you start the test system:

```console
docker login --username <your_user_id> --password <your_password>
```

<sub>*The user-id and password needed to pull the docker image of our service is provided to you by us.</sub>

and

```console
docker compose --project-name customer_service_system --file docker-compose.yml --env-file config.env up
```

If no error arises, the system runs and is already fully functional.


## Deploying Test Data

The test system contains a MS SQL Server.
You might restore a database backup to get some data to play with.


## Debugging

### Postman

You can call the API without the need to implement an API client by using a testing tool like [Postman](https://www.postman.com) which kindly supports gRPC.
