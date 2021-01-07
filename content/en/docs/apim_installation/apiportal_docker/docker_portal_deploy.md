{
  "title": "Build API Portal image using Dockerfile",
  "linkTitle": "Build using Dockerfile",
  "weight": "40",
  "date": "2019-08-09",
  "description": "Build an API Portal Docker image using the Dockerfile available in the sample package."
}

MySQL image is not included with the API Portal Docker sample package. You must download it separately from [Docker Hub](https://hub.docker.com/).

## Prerequisites

* [Docker engine](https://docs.docker.com/engine/).
* API Portal Docker sample package, available from [Axway Support](https://support.axway.com).
* MySQL server.

A running MySQL server is required to build API Portal image. During the build process, a new database is created, and it is deleted automatically when the build is finished.

## Download API Portal Docker sample package

You can download the API Portal Docker sample package from [Axway Support](https://support.axway.com/).

The package structure is as follows:

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

## Build your image with Two-Step build

You can build your API Portal docker image following a Two-Step build:

1. Build API Portal base image with all the software API Portal runtime relies on.
2. Extend API Portal base image with API Portal software.

<!--
API Portal docker image build involves multiple build stages, which can be split in 2 steps:

1. Build API Portal infrastructure image with all the software API Portal runtime relies on.
2. Extend API Portal infrastructure image with API Portal software.

The goal of [2-steps build](#2-steps-build) is to build and capture the first step and install API Portal on top of it with the second step. Thus, we can reuse image from the first step multiple times for newer API Portal versions.

2-steps build involves 2 dockerfiles:

* `dockerfiles/base.Dockerfile`
* `dockerfiles/web.Dockerfile`
-->

To build the base image, run the following command using the `dockerfiles/base.Dockerfile`:

```
docker image build -t <base-image-tag> \
  -f dockerfiles/base.Dockerfile <docker-build-context-directory>
```

Now, build API Portal image from the base image using the `dockerfiles/web.Dockerfile`:

```
docker image build -t <apiportal-image-tag> \
  --build-arg APIPORTAL_BASE_IMG=<base-image-tag> \   # Base image name. Used only with Two-Step build.
  --build-arg MYSQL_HOST=<mysql-build-host> \
  --build-arg MYSQL_PORT=<mysql-build-host-port> \
  --build-arg MYSQL_DATABASE=<mysql-build-host-db-name> \
  --build-arg MYSQL_USER=<mysql-build-host-user> \
  --build-arg MYSQL_PASSWORD=<mysql-build-host-user-pass> \
  --build-arg THE_UID=<optional-custom-uid> \
  --build-arg THE_GID=<optional-custom-uid> \
  -f dockerfiles/web.Dockerfile <docker-build-context-directory>
```

## Build your image with a Single-Step build

You can also build API Portal docker image following a Single-Step, but in this case, it will only produce one tagged image, so you will not have a base image to reuse later.

<!-- 
In contrast with the [2 steps build](#2-steps-build), **single step build** process happens in one command and produces only 1 tagged image. **Single step build** involves only `Dockerfile`, so you can omit `-f` directive of `docker image build` command. 
-->

To build API Portal docker image following a Single-Step build, run the following command:

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

The Two-Step build does not expect any arguments, but for the Single-Step build the following arguments are used:

* `MYSQL_HOST` (required) - API Portal uses this MySQL host to create the initial database dump file.
* `MYSQL_PORT` (required) - MySQL server port.
* `MYSQL_DATABASE` (required) - Database name. If this database exists on the server it will be reset, if it does not exist yet, it will be created. Ensure that MySQL user has privileges to create and drop this database.
* `MYSQL_USER` (required) - MySQL user.
* `MYSQL_PASSWORD` (required) - MySQL user password.
* `THE_UID` and `THE_GID` (optional) - This changes the default group ID and user ID of the Apache user inside the container. Defaults to `1048` for both. Values lower than `1000` are **not** recommended.

Only `MYSQL_*` arguments are required. API Portal docker image cannot be build without MySQL connection.

## Two-Step and Single-Step scripts

The following is an example of a Two-Step build script:

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

The following is an example of a Single-Step build script:

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
