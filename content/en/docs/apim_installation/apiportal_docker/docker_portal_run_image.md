{
    "title":"Run API Portal using ready-made Docker image",
    "linkTitle":"Run using ready-made Docker image",
    "weight":"2",
    "date":"2019-08-09",
    "description":"Use the ready-made API Portal Docker image to run in Docker containers."
}

This topic describes how to use the ready-made API Portal Docker image to run in Docker containers. The image is ready out-of-the-box, so you do not have to build it using the `Dockerfile`.

## Prerequisites

The following components are required on your system before you can deploy API Portal in Docker containers:

* [Docker engine][docker engine]
* MySQL server
* API Portal Docker image available from [Axway Support][axway support]
* API Gateway and API Manager either installed on-premise or deployed in containers (see the [API Gateway Installation Guide](/docs/apim_installation/apigtw_install/) for more details). API Gateway and API Manager are not required to be installed in order to run API Portal, you can install them and configure in API Portal later
* Redis server (optional)

The monitoring feature of API Portal, which enables your API consumers to monitor application and API usage, requires a connected API Manager with monitoring metrics enabled.

The following are the recommended hardware disk space and memory requirements for the Docker host machine for a single node sample architecture:

* 100 GB or more disk space
* 8 GB or more RAM

## Run a Docker container using the image

1. Download the API Portal Docker image from [Axway Support][axway support].
2. Upload the file to your Docker host machine.
3. Enter the following command to load the image:

    `docker load -i APIPortal_7.7_Docker_Image_linux-x86-64_<build number>.tgz`

4. Run the API Portal Docker container, for example:

    ```
    docker container run --name apiportal \
      -d -p 8080:80 \
      -e MYSQL_HOST=mysql.axway.com \
      -e MYSQL_PORT=3306 \
      -e MYSQL_DATABASE=joomla \
      -e MYSQL_USER=joomla \
      -e MYSQL_PASSWORD=XXXXX \
      apiportal:7.7
    ```

    This example performs the following:

    * Runs an API Portal Docker container from an image named `apiportal`:`7.7` in detached mode.
    * Sets environment variables for connecting to the MySQL server.
    * Binds port 80 of the container to port 8080 on the host machine.

API Portal is now running in a Docker container.

Before you can use API Portal, you must link it to your API Manager. For more details, see [Connect API Portal to API Manager](/docs/apim_installation/apiportal_install/connect_to_apimgr/).

## Environment variables

API Portal container supports a wide range of environment variables that allows you configure API Portal runtime and partially JAI settings.

### Supported environment variables list

The following is a comprehensive and heavily commented snippet that can be directly copy-pasted to your _env_ file.

    ##### NOTE #####
    # Boolean environment variables can take a value of 0 or 1.
    # `*_CONFIGURED` and `*_ON` variables are boolean.
    ################

    ##### REQUIRED SETTINGS #####
    # This configuration settings are required for API Portal
    # docker container to boot.
    #############################

    MYSQL_HOST=
    MYSQL_PORT=3306
    MYSQL_DATABASE=
    MYSQL_USER=
    MYSQL_PASSWORD=

    ##### OPTIONAL SETTINGS #####
    # The rest of configuration settings are optional.
    #############################

    # Certificates can be passed in plain text or as base64 encoded string.
    # Example:
    # APACHE_SSL_CERT=base64:<base64-encoded-certificate>
    # APACHE_SSL_PRIVATE_KEY=<plain-text-private-key>
    APACHE_SSL_ON=0
    APACHE_SSL_CERT=
    APACHE_SSL_PRIVATE_KEY=

    ##### CHANGABLE SETTINGS #####
    # The rest of configuration settings can be configured in JAI as well.
    # `*_CONFIGURED` option determins if the feature is configured with
    # environment variables, for example `APIMANAGER_CONFIGURED=0` means
    # that the rest of `APIMANAGER_*` variables won't effect the runtime.
    # On the other hand `APIMANAGER_CONFIGURED=1` will configure API Manager
    # with values from environment variables.
    #
    # !!! With `*_CONFIGURED` option set to 1 all the changes made in JAI will be
    # overriden by values from environment variables on the container restart
    #
    # `*_ON` option determins whether the feature is enabled or not
    ##############################

    # For reference see "Connect API Portal to a single API Manager"
    # under "Connect API Portal to API Manager" page in API Portal docs
    APIMANAGER_CONFIGURED=0
    APIMANAGER_NAME=Master
    APIMANAGER_HOST=
    APIMANAGER_PORT=8075

    # For reference see "Customize Try-it by type of request"
    # under "Customize API Catalog" page in API Portal docs.
    # All `TRYIT_METHODS_*` vars are boolean
    TRYIT_METHODS_CONFIGURED=0
    TRYIT_METHODS_ENABLE_GET=1
    TRYIT_METHODS_ENABLE_POST=1
    TRYIT_METHODS_ENABLE_PUT=1
    TRYIT_METHODS_ENABLE_DELETE=1
    TRYIT_METHODS_ENABLE_PATCH=1
    TRYIT_METHODS_ENABLE_HEAD=1
    TRYIT_METHODS_ENABLE_OPTIONS=1

    # For reference see reCapcha related topics
    # under "Additional customizations" page in API Portal docs
    # `LOGIN_PROTECTION_LOCK_IP` is boolean
    LOGIN_PROTECTION_CONFIGURED=0
    LOGIN_PROTECTION_ON=0
    LOGIN_PROTECTION_ATTEMPTS_BEFORE_LOCK=3
    LOGIN_PROTECTION_ATTEMPTS_BEFORE_RECAPCHA=3
    LOGIN_PROTECTION_LOCK_DURATION_SEC=600
    LOGIN_PROTECTION_LOCK_IP=0

    # for reference see "API Portal single sign-on"
    # page in API Portal docs
    SSO_CONFIGURED=0
    SSO_ON=0
    SSO_PATH=
    SSO_ENTITY_ID=
    SSO_WHITELIST=

    # for reference see "Secure API Portal"
    # page in API Portal docs
    OAUTH_WHITELIST_CONFIGURED=0
    # Comma separated string
    OAUTH_WHITELIST=

    # for reference see "Secure API Portal"
    # page in API Portal docs
    API_WHITELIST_CONFIGURED=0
    # Comma separated string
    API_WHITELIST=

    ##### NON PERSISTING SETTINGS #####
    # Settings under this secrtion don't persist. I.e. if you configure
    # it in JAI they will be gone after container restart. So in common
    # use case they should be configured via environment variables.
    ###################################

    # for reference see "Install Redis cache"
    # page in API Portal docs
    REDIS_CONFIGURED=0
    REDIS_ON=0
    REDIS_HOST=
    REDIS_PORT=6379
    REDIS_CACHE_TIMEOUT_SEC=600

You can copy these variables to an _env_ file, edit the values and use it for `docker run` command. Inline environment variables take precedence over the ones from _env_ file.

Demo (assuming variables are in `.env` file):

    docker container run --env-file .env \
      -e MYSQL_PASSWORD=very_secret_password \
      -e APACHE_SSL_PRIVATE_KEY="$(cat ~/certs/apiportal.key)" \
      <more-options...>

In this case `very_secret_password` and certificate taken from `apiportal.key` file will override the password and certificate in the `.env` file.

## Data persistence

By default, API Portal container doesn't create any volumes for data persistence. You may want to create Docker data volumes to persist API Portal customization data. Using data volumes can also prevent data loss when the container reboots or crashes, or when you are upgrading or setting up HA for an API Portal Docker deployment. On the other hand there is no need for data volumes if you run API Portal container for a quick demo or test.

The data volumes are stored on the Docker host machine and as such consume disk space. You should delete unused data volumes regularly.

### Data volume candidates list

The following list describes which API Portal assets should be stored in a Docker volume to preserve the customizations during upgrade or HA setup of an API Portal Docker deployment.

* `/opt/axway/apiportal/enckey` - encryption key directory. Used by Public API mode.
* `/opt/axway/apiportal/htdoc/images` - images uploaded by API Portal users or admins.
* `/opt/axway/apiportal/htdoc/language` - API Portal translations.
* `/opt/axway/apiportal/htdoc/templates` - Joomla! templates.
* `/opt/axway/apiportal/htdoc/administrator/language` - Joomla! admin panel translations.
* `/opt/axway/apiportal/htdoc/administrator/components/com_apiportal/assets/cert` - certificates for API Manager.

### Demo
    # create volumes
    docker volume create apiportal-enckey
    docker volume create apiportal-images
    docker volume create apiportal-language
    docker volume create apiportal-templates
    docker volume create apiportal-adm-language
    docker volume create apiportal-certs

    # start API Portal container using the created volumes
    docker container run \
      -v apiportal-enckey:/opt/axway/apiportal/enckey \
      -v apiportal-images:/opt/axway/apiportal/htdoc/images \
      -v apiportal-language:/opt/axway/apiportal/htdoc/language \
      -v apiportal-templates:/opt/axway/apiportal/htdoc/templates \
      -v apiportal-adm-language:/opt/axway/apiportal/htdoc/administrator/language \
      -v apiportal-certs:/opt/axway/apiportal/htdoc/administrator/components/com_apiportal/assets/cert \
      <more-options>

[docker engine]: https://docs.docker.com/engine/
[axway support]: https://support.axway.com
