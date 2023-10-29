# Customer API

This API provides and encapsulates access to the *Customer* data persisted in internal databases, one for each *Praxis Group*.

Users of this API can manage their data via this API to combine Henara services with their own applications.


## Test System

You can test the API with a self hosted test system which is based on the [docker compose](https://docs.docker.com/compose) technology.

So you need a docker host. Among various methods you could install [Docker Desktop](https://www.docker.com/products/docker-desktop) to run a docker host on your desktop machine.

With the files *docker-compose.yml* and *config.env* (provided in this folder), and *config.env* updated to your needs, you start the test system:

```console
docker login --username henara --password <your_access_token>
```

<sub>*The access token needed to pull the docker image of our service is provided to you by us.</sub>

and

```console
docker compose --project-name customer_service_system --file docker-compose.yml --env-file config.env up
```

If no error arises, the system runs but requires importing a database backup.


## Deploying Test Data

The test system contains a MS SQL Server.
You need to restore a database backup to get some data to play with.

## Encryption

The gRPC-API performs server authentication SSL/TLS transport encryption using a private key and a certificate.

In case you access the test system at *localhost*, keys and a self signed certificate can be generated like this:

```bash
# generate key and certificate
openssl req -x509 -out localhost.crt -keyout localhost.key -newkey rsa:2048 -nodes -sha256 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")

# place keys and certificate into a .pfx container
openssl pkcs12 -export -in localhost.crt -inkey localhost.key -out localhost.pfx
```

The certificate can be added to the client systems collection of trusted root certificates.

The customer service application requires information about the *.pfx* file (containing the private key and the certificate) via the configuration key *grpc:pfx_path* and *grpc:pfx_password*.
The provided test system defines a file mapping in *docker-compose.yml* and the service configuration in *config.env*.


## Authentication

Each call to the gRPC-API requires authentication.
To authenticate, clients use the HTTP-header *"access_token: <access_token>"*. In gRPC this is a value in the metadata of the request.

The access token is a base64-encoded GUID which is set in the test services *config.env*.

[This online tool](https://toolslick.com/conversion/data/guid) works fine for GUID format conversions.

When using *Postman* for API testing, metadata are editable within the UI.

Please refer to the general gRPC documentation or [vendor specific documentation](https://learn.microsoft.com/en-us/dotnet/architecture/grpc-for-wcf-developers/channel-credentials) on how to edit call metadata.


## Debugging

### Postman

You can call the API without the need to implement an API client by using a testing tool like [Postman](https://www.postman.com) which kindly supports gRPC.

When using *Postman* for API testing, metadata are editable within the UI.
