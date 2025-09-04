# Connectors

Just like you manage Connectors through the website, you can also manage them via the API. This section describes exactly how to do this. All endpoints described here are protected.

## Create Connectors

You can create a Connector by sending a `POST` request to `/connectors/<your-chosen-connector-name>`.

The payload must be provided as a `JSON`. If you intend on only using the `API` you can simply use the `HttpData` payload. However, if you want to also use this Connector via the website you need to provide correct storage credentials in the payload.

After a successful request the Connector will be created and begin to start up.

### HttpData

```json
{
    "storage_type": "HttpData",
    "storage_config": {}
}
```

### AmazonS3

For explanations on the exact values you need to provide, please refer to the website documentation.

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

### AzureStorage

For explanations on the exact values you need to provide, please refer to the website documentation.

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

## Edit Connectors

Simlarly to creating a Connector you can edit a Connector by sending a `PUT` request to `/connectors/<connector-name>`. The payload you need to provide here is exactly the same as for creating a Connector. After a successful request the Connector will restart using the newly provided configuration.

## Get Connectors

You can get a list of all your Connectors by sending a `GET` request to `/connectors`. If you want to get only a specific Connector you can send a `GET` request to `/connectors/<connector-name>`.

## Start and Stop Connectors

To start and stop a Connector you can send a `GET` request to `/connectors/<connector-name>/start` and `/connectors/<connector-name>/stop` respectively.

## Fail Connectors

In some cases a Connector might be stuck in some unwanted state because of a bug. If that is the case you can get the Connector into the `FAILED` state by sending a `GET` request to `/connectors/<connector-name>/fail`. From there you can either stop or delete the Connector. Note, however, that this does not necessarily mitigate the bug.
