{
    "title":"Upgrade API Portal docker deployment",
    "linkTitle":"Upgrade docker deployment",
    "weight":"30",
    "date":"2021-01-05",
    "description":"Upgrade your API Portal Docker deployment, preserving any API Portal customizations."
}

This topic describes how to upgrade an API Portal Docker deployment. The upgrade preserves any API Portal customizations stored in volumes or database.

## Upgrade steps

In order to upgrade API Portal container to a newer version do the following:

* Obtain a newer API Portal Docker image.
* Remove the running container by issuing the following command:
  ```
  docker container rm -f <old-container-name>
  ```
* Recreate a new container with the same docker run parameters as the old one with the command:
  ```
  docker container run <old-parameters> <newer-image>
  ```

Keep in mind that there is no support for downgrading of API Portal container. Running an older API Portal container against a newer database schema will result in a failure.
