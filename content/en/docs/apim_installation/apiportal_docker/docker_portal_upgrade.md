{
    "title":"Upgrade API Portal docker deployment",
    "linkTitle":"Upgrade docker deployment",
    "weight":"30",
    "date":"2021-01-05",
    "description":"Upgrade your API Portal Docker deployment while preserving any API Portal customizations stored in volumes or database."
}

To upgrade API Portal container to a newer version, perform the following:

1. Obtain a newer API Portal Docker image.
2. Remove the running container:

    ```
    docker container rm -f <old-container-name>
    ```

3. Recreate a new container with the same docker run parameters as the old one:

    ```
    docker container run <old-parameters> <newer-image>
    ```

{{% alert title="Note" %}}
There is no support for downgrading of API Portal container. Running an older API Portal container against a newer database schema will result in failure.
{{% /alert %}}
