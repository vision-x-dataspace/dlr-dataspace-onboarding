# Creating an Asset

## Introduction

An Asset is the fundamental representation of an arbitrary backend interface in the EDC. The Data Provider registers it with its Control Plane as a first step to expose it to the Dataspace via the Dataplane later on. This registration is executed via the following request:

## Request

```http
POST /v3/assets HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/<your-connector-name>/management
X-Api-Key: <your-password>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-password>` with your password.

```json
{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@id": "<asset-id>",
  "properties": {
    "name": "test-asset"
  },
  "privateProperties": {
    "secret_value": "my_secret"
  },
  "dataAddress": {
    "@type": "DataAddress",
    "type": "AmazonS3",
    "keyName": "<file-name-in-storage>",
    "region": "us-east-1",
    "bucketName": "<bucket-name>",
    "endpointOverride": "<storage-url>",
    "accessKeyId": "<storage-username>",
    "secretAccessKey": "<storage-password>"
  }
}
```

Replace the strings surrounded by `<>` with the correct values for your setup (`<asset-id>` is arbitrary). Creating the bucket and uploading the file has to be done manually.

## Explanation

The `@id` parameter will identify the configured endpoint access permanently. This is the same id that a data consumer will see when being presented the corresponding data offers when retrieving the catalog.

Additionally, there is the possibility to add `properties` and `privateProperties` to the Asset. The former are exposed in the catalog to potential Data Consumers. Private properties, however, can only be seen by the Data Provider.

Most consequential however is the `dataAddress` section of the asset-APIs payload. It establishes a reference to some file, service, etc. that is supposed to be offered. In the above example this is merely a dummy for purposes of this tutorial.

Below is the example `dataAddress` referencing a file in an `AmazonS3` file storage used above.

```
"dataAddress": {
    "@type": "DataAddress",
    "type": "AmazonS3",
    "keyName": "my_file.txt",
    "region": "us-east-1",
    "bucketName": "my_bucket",
    "endpointOverride": "http://my-storage.com",
    "accessKeyId": "my_key_id",
    "secretAccessKey": "my_secret_key"
}
```

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/01_assets.md).
