{
  "title": "Run API Portal using Docker Compose",
  "linkTitle": "Run using Docker Compose",
  "weight": "50",
  "date": "2021-01-05",
  "description": "Run an API Portal using `docker-compose.yml` in the sample package."
}

This section describes how to run API Portal Docker container with Docker Compose tool using sample `docker-compose.yml`.

Docker Compose is a simple way to run the whole API Portal solution with a single command.

## Requirements

* [Docker engine](https://docs.docker.com/engine/)
* [Docker Compose](https://docs.docker.com/compose/)
* API Portal Docker image, available from [Axway Support](https://support.axway.com)
* API Portal Docker sample package, available from [Axway Support](https://support.axway.com)

## What is included

In the `docker-compose.yml` file provided in the API Portal Docker sample package we provide following services preconfigured:

* MariaDB
* Redis
* API Portal

I.e. by running this configuration you don't need to worry about MariaDB and Redis installation and configuration, they are ready to be used with API Portal out of the box.

## What is not included

The `docker-compose.yml` file doesn't include API Manager and ClamAV configurations. You can set them up and configure in API Portal separately. API Portal can't serve its purpose without API Manager, but ClamAV is a completely optional security tool.

## Simple deployment example

### Edit docker-compose.yml

Open `docker-compose.yml` file in an editor and locate there `image` section under `apiportal` service. Change the value to the name of your API Portal docker image.

```
# ...
services:
# ...
  apiportal:
    image: <your-api-portal-image>
```

### Start the services

Run

```
docker-compose up -d
```

and wait API Portal service to get loaded. You can check readiness with the following command:

```
docker-compose ps apiportal
```

When you see `Up (healthy)` under **State** column it means API Portal is ready to handle requests.

If API Portal container doesn't become available within 30 seconds after `up` command, check logs for issues with the command:

```
docker-compose logs apiportal
```

## Editing docker-compose.yml

`docker-compose.yml` in this package is for demo purpose only. You can modify it up to your needs. You can also modify [`sample.env`](sample.env) file or replace it with your own one in `env_file` section under `apiportal` service.

Some useful links:

* [Compose file reference](https://docs.docker.com/compose/compose-file/)
* [Environment variables in Compose](https://docs.docker.com/compose/environment-variables/)
* [Use Compose in production](https://docs.docker.com/compose/production/)
