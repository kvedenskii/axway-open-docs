{
  "title":"Troubleshooting API Portal in Docker",
  "linkTitle":"Troubleshooting",
  "weight":"4",
  "date":"2019-08-09",
  "description":"Troubleshoot problems you might encounter when running API Portal in Docker containers."
}

As API Portal in docker is relativly close to on-premise API Portal, this section describes only docker related issues. For the rest please visit [Troubleshooting API Portal](/docs/apim_administration/apiportal_admin/troubleshooting/) section.

## Checking logs

API Portal container redirects Apache and API Portal logs to stdout and stderr. That means that you can view the logs with

    docker container logs -f <container-name>

Alternatively you can run API Portal in non-detached mode, i.e. without `-d` flag. This will let you see logs in realtime from the very beginning of the container boot. Not recommended for production, only for testing.

In most cases logs help to detect the problem cause.

## Apache does not start

After the API Portal container is started, the Apache service is not started and you cannot access your API Portal.

Verify that you have waited sufficient time for the container to start. When running the container for the first time depending on your database load and connection speed it can take a while to import the whole database schema and initial data.

To check if this is the case, check the Docker logs for the API Portal container.

## API Portal UI does not load

When you try to access API Portal from a browser you get the following message: `Error displaying the error page.`

Perform the following checks to try and identify the cause of the problem:

* Check whether the database is running and the API Portal schema is available.
* Connect to the API Portal container and check whether it can access the database schema from the database container.
* Connect to the API Portal container and open `/opt/axway/apiportal/htdoc/configuration.php` and verify that the database settings are correct (host, port, user, password, db, and so on).
* If you cannot identify the cause of the problem, contact [Axway Support][axway support].

[axway support]: https://support.axway.com
