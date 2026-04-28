# Connectors

Just like you manage connectors through the website, you can also manage them via the API. This section describes exactly how to do this.

!!! warning "Protected Endpoints"
    All endpoints described on this page require authentication. Make sure to include your API key as a bearer token in the `Authorization` header of every request.

## Create Connector

Send a request with a JSON payload describing the storage backend your connector should use.

```http
POST /connectors/<your-chosen-connector-name>
```

| Storage Type | Storage |
|--------------|----------|
| `HttpData` | No external storage |
| `AmazonS3` | S3-compatible storage |
| `AzureStorage` | Azure Blob Storage |

!!! info "Storage"
    The choice of storage type is only relevant for usage via the website. It is possible to connect any type of storage dynamically regardless of choice of storage type.

=== "HttpData"

    ```json
    {
        "storage_type": "HttpData",
        "storage_config": {}
    }
    ```

    !!! tip
        No storage credentials required. Use this if you only interact with the connector via the API.

=== "AmazonS3"

    ```json
    {
        "storage_type": "AmazonS3",
        "storage_config": {
            "bucket_name": "<bucket-name>",
            "region": "<region>",
            "url": "<url>",
            "username_read": "<username-read>",
            "password_read": "<password-read>",
            "username_write": "<username-write>",
            "password_write": "<password-write>"
        }
    }
    ```

    !!! warning "Storage Access"
        Needs an S3-compatible storage to be accessible via the given credentials.

=== "AzureStorage"

    ```json
    {
        "storage_type": "AzureStorage",
        "storage_config": {
            "container_name": "<container-name>",
            "region": "<region>",
            "url": "<url>",
            "account_name_read": "<account-name-read>",
            "account_key_read": "<account-key-read>",
            "account_name_write": "<account-name-write>",
            "account_key_write": "<account-key-write>"
        }
    }
    ```

    !!! warning "Storage Access"
        Needs an Azure Blob Storage to be accessible via the given credentials.

## Edit Connector

Similar to creation, you can also edit a connector. The payload is identical in structure to the one used when creating a connector.

```http
PUT /connectors/<connector-name>
```

!!! info "Restart"
    After a successful request the connector will automatically restart using the newly provided configuration.

## Get Connectors

You can also retrieve information on all your connector or a specific connector.

```http
GET /connectors
GET /connectors/<connector-name>
```

## Start, Stop, and Fail a Connector

These endpoints let you control the runtime state of a connector.

| Action | Endpoint |
|--------|----------|
| Start | `PUT /connectors/<connector-name>/start` |
| Stop | `PUT /connectors/<connector-name>/stop` |
| Fail | `PUT /connectors/<connector-name>/fail` |

!!! warning "Using Fail"
    Keep in mind that failing a connector does **not** necessarily fix the underlying bug. It is purely a recovery mechanism to regain control over the connector.

## Code Examples

=== "Create Connector (AmazonS3)"

    === "curl"

        ```bash
        curl -X POST "https://vision-x-api.base-x-ecosystem.org/connectors/alice" \
        -H "Authorization: Bearer sk-..." \
        -H "Content-Type: application/json" \
        -d '{
            "storage_type": "AmazonS3",
            "storage_config": {
            "bucket_name": "alice-backup-bucket",
            "region": "us-east-1",
            "url": "https://s3.my.aws.com",
            "username_read": "alice_read_user",
            "password_read": "alice_read_pass123",
            "username_write": "alice_write_user",
            "password_write": "alice_write_pass456"
            }
        }'
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice"
        headers = {
            "Authorization": "Bearer sk-...",
            "Content-Type": "application/json",
        }
        payload = {
            "storage_type": "AmazonS3",
            "storage_config": {
                "bucket_name": "alice-backup-bucket",
                "region": "us-east-1",
                "url": "https://s3.my.aws.com",
                "username_read": "alice_read_user",
                "password_read": "alice_read_pass123",
                "username_write": "alice_write_user",
                "password_write": "alice_write_pass456"
            }
        }

        response = requests.post(url, json=payload, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```


=== "Start Connector"

    === "curl"

        ```bash
        curl -X PUT "https://vision-x-api.base-x-ecosystem.org/connectors/alice/start" \
        -H "Authorization: Bearer sk-..."
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/start"
        headers = {"Authorization": "Bearer sk-..."}

        response = requests.put(url, json=payload, headers=headers)
        response.raise_for_status()
        ```

=== "Stop Connector"

    === "curl"

        ```bash
        curl -X PUT "https://vision-x-api.base-x-ecosystem.org/connectors/alice/stop" \
        -H "Authorization: Bearer sk-..."
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/stop"
        headers = {"Authorization": "Bearer sk-..."}

        response = requests.put(url, json=payload, headers=headers)
        response.raise_for_status()
        ```
