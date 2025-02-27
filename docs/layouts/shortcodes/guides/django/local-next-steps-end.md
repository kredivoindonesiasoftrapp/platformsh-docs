3.  Commit and push the revisions by running the following command:

    ```bash
    git add . && git commit -m "Add local configuration" && git push platform local-config
    ```

4.  Merge the change into production by running the following command:

    ```bash
    platform merge local-config
    ```

Once the script is merged into production,
any user can then set up their local environment by running the following commands:

```bash
{{ `$ platform get {{< variable "PROJECT_ID" >}}
$ cd {{< variable "PROJECT_NAME" >}}
$ ./init-local.sh {{< variable "PROJECT_ID" >}} another-new-feature main` | .Page.RenderString }}
```

### Sanitize data

It's often a compliance requirement to ensure that only a minimal subset of developers within an organization
have access to production data during their work.
By default, your production data is automatically cloned into _every_ child environment.

You can customize your deployments to include a script that sanitizes the data within every non-production environment. 

1.  Create a new environment called `sanitize-non-prod`.

2.  Follow the example on how to [sanitize PostgreSQL with Django](../../../development/sanitize-db/postgresql.md).
    This adds a sanitization script to your deploy hook that runs on all non-production environments.

3.  Commit and push the revisions by running the following command:

    ```bash
    git add . && git commit -m "Add data sanitization" && git push platform sanitize-non-prod
    ```

4.  Merge the change into production by running the following command:

    ```bash
    platform merge sanitize-non-prod
    ```

Once the script is merged into production, every non-production environment created on Platform.sh
and all local environments contain sanitized data free of your users' personally identifiable information (PII).
