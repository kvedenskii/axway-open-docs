{
  "title": "Build API Portal image using Dockerfile",
  "linkTitle": "Build using Dockerfile",
  "weight": "40",
  "date": "2019-08-09",
  "description": "Build an API Portal Docker image using the `Dockerfile` in the sample package."
}

This section describes how to build an API Portal Docker image using the `Dockerfile` in the sample package.

MySQL image is not included with the API Portal Docker sample package. You must download it separately from [Docker Hub](https://hub.docker.com/).

## Prerequisites

* [Docker engine](https://docs.docker.com/engine/)
* API Portal Docker sample package, available from [Axway Support](https://support.axway.com)
* MySQL server

In order to build API Portal image you need a running MySQL server. During the build process a new database will be created. It will be deleted automatically when the build is over.

## API Portal Docker sample package

You can download the API Portal Docker sample package from Axway Support at [https://support.axway.com](https://support.axway.com/).

The package structure is following:

```
├── dockerfiles/          - 2-steps build dockerfiles
│   ├── base.Dockerfile
│   └── web.Dockerfile
├── rootfs/               - assets required for building API Portal docker image
│   ├── apiportal-build/
│   ├── apiportal-web/
│   ├── webserv-base/
│   └── webserv-build/
├── docker-compose.yml    - demo docker compose manifest
├── Dockerfile            - single step build dockerfile
├── .dockerignore         - dockerignore
├── README*.md            - readme files for API Portal in docker build and usage
└── sample.env            - sample environment variables file
```

## 2-steps build

API Portal docker image build involves multiple build stages. Virtually we can split them into 2 steps:

* Build API Portal infrastructure image with all the software API Portal runtime relies on.
* Extend API Portal infrastructure image with API Portal software.

The goal of [2-steps build](#2-steps-build) is to build and capture the first step and install API Portal on top of it with the second step. Thus, we can reuse image from the first step multiple times for newer API Portal versions.

2-steps build involves 2 dockerfiles:

* `dockerfiles/base.Dockerfile`
* `dockerfiles/web.Dockerfile`

### Build base image

```
docker image build -t <base-image-tag> \
  -f dockerfiles/base.Dockerfile <docker-build-context-directory>
```

### Build API Portal image from base

```
docker image build -t <apiportal-image-tag> \
  --build-arg APIPORTAL_BASE_IMG=<base-image-tag> \
  --build-arg MYSQL_HOST=<mysql-build-host> \
  --build-arg MYSQL_PORT=<mysql-build-host-port> \
  --build-arg MYSQL_DATABASE=<mysql-build-host-db-name> \
  --build-arg MYSQL_USER=<mysql-build-host-user> \
  --build-arg MYSQL_PASSWORD=<mysql-build-host-user-pass> \
  --build-arg THE_UID=<optional-custom-uid> \
  --build-arg THE_GID=<optional-custom-uid> \
  -f dockerfiles/web.Dockerfile <docker-build-context-directory>
```

## Single step build

In contrast with the [2-steps build](#2-steps-build), **single step build** process happens in one command and produces only 1 tagged image. It's nothing more than both steps from [2-steps build](#2-steps-build) combined.

**Single step build** involves only `Dockerfile`, so you can omit `-f` directive of `docker image build` command.

### Build API Portal image

```
docker image build -t <apiportal-image-tag> \
  --build-arg MYSQL_HOST=<mysql-build-host> \
  --build-arg MYSQL_PORT=<mysql-build-host-port> \
  --build-arg MYSQL_DATABASE=<mysql-build-host-db-name> \
  --build-arg MYSQL_USER=<mysql-build-host-user> \
  --build-arg MYSQL_PASSWORD=<mysql-build-host-user-pass> \
  --build-arg THE_UID=<optional-custom-uid> \
  --build-arg THE_GID=<optional-custom-uid> \
  <docker-build-context-directory>
```

## Build arguments

The first build step in the [2 steps build](#2-steps-build) doesn't expect any arguments. For the second build step or single step build the following arguments are used:

* `APIPORTAL_BASE_IMG` - base image name, can be used only with [2-steps build](#2-steps-build).
* `MYSQL_HOST` (required) - MySQL host for building API Portal image. It's required in order API Portal to create initial database dump file only.
* `MYSQL_PORT` (required) - MySQL server port.
* `MYSQL_DATABASE` (required) - database name. If this database exists on the server it will be reset, if it doesn't exist it will be created. MySQL user should have privileges to create and drop this database.
* `MYSQL_USER` (required) - MySQL user.
* `MYSQL_PASSWORD` (required) - MySQL user password.
* `THE_UID` and `THE_GID` (optional) - change default group ID and user ID of the Apache user inside the container. Default is 1048 for both. Be reasonable with these values, in general values lower than 1000 are **not** recommended.

Only `MYSQL_*` arguments are required. API Portal docker image can't be build without MySQL connection.

## Demo

2-steps build:

```
# build base image
docker image build -t axway/apiportal-base:X.X.X \
  -f dockerfiles/base.Dockerfile .
# build API Portal image
docker image build -t axway/apiportal:X.X.X \
  --build-arg APIPORTAL_BASE_IMG=axway/apiportal-base:X.X.X \
  --build-arg MYSQL_HOST=mysql.jenkins.axway.com \
  --build-arg MYSQL_PORT=3306 \
  --build-arg MYSQL_DATABASE=apiportal_build \
  --build-arg MYSQL_USER=you_dont_know_him \
  --build-arg MYSQL_PASSWORD=youll_never_guess \
  --build-arg THE_UID=1024 \
  --build-arg THE_GID=1025 \
  -f dockerfiles/web.Dockerfile .
```

Single step build:

```
docker image build -t axway/apiportal:X.X.X \
  --build-arg MYSQL_HOST=mysql.jenkins.axway.com \
  --build-arg MYSQL_PORT=3306 \
  --build-arg MYSQL_DATABASE=apiportal_build \
  --build-arg MYSQL_USER=you_dont_know_him \
  --build-arg MYSQL_PASSWORD=youll_never_guess
  --build-arg THE_UID=1024 \
  --build-arg THE_GID=1025 .
```
