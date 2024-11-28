# Initiating a Transfer Process

## Introduction

Despite the naming, the Transfer Process is not the step that transmits the backend's data from the Provider to the Consumer. What this API does instead is trigger the Transfer of a Data Plane token from the Provider Control Plane to the Consumer Control Plane and in turn to a location specified by the Data Consumer.

## Request

```http
POST /v2/transferprocesses HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/<your-connector-name>/management
Authorization: Bearer <your-token>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-token>` with your token.

```json
{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/",
    "odrl": "http://www.w3.org/ns/odrl/2/"
  },
  "assetId": "<asset-id>",
  "connectorAddress": "<dcat:service.dct:endpointUrl>",
  "contractId": "<contractAgreementId>",
  "dataDestination": {
    "type": "AmazonS3",
    "keyName": "<file-name-in-storage>",
    "bucketName": "<bucket-name>",
    "region": "us-east-1",
    "endpointOverride": "<storage-url>",
    "accessKeyId": "<storage-username>",
    "secretAccessKey": "<storage-password>"
  },
  "protocol": "dataspace-protocol-http",
}
```

Once again replace the values surrounded by `<>` with the correct values for your setup. For the values in `dataDestination` it should now be the ones for the other storage / bucket. Also, note down the received `@id`.

## Explanation

- `assetId` is the id of the Asse that a transfer process should be triggered for.
- `connectorAddress` is the DSP-endpoint of the Data Provider.
- `contractId` represents the Contract Agreement that the Provider and Consumer agreed on during the Contract Negotiation
  phase.
- `dataDestination` will in the case of an HTTP-based transfer of the Token be a `DataAddress` object, holding exclusively
  the `type` property that must be set to `"HttpProxy"`.
- `protocol` describes the protocol between the EDCs and will always be `dataspace-protocol-http`.

This call also returns an id, that can be used to monitor the progress.

```json
{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@id": "177aba51-52d7-44dc-beab-fd6151147024",
  "createdAt": 1688465655
}
```

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/06_transferprocesses.md).

## Checking for Completion

```http
GET /v2/transferprocesses/<@id> HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/<your-connector-name>/management
Authorization: Bearer <your-token>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-token>` with your token. Also, replace `<@id>` by the ID revieved from above.

The returned details for the transfer should look something like this:

```json
{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "https://w3id.org/edc/v0.0.1/ns/TransferProcess",
  "@id": "process-id",
  "correlationId": "correlation-id",
  "type": "PROVIDER",
  "state": "COMPLETED",
  "stateTimestamp": 1688465655,
  "assetId": "<asset-id>",
  "connectorId": "<providerId>",
  "contractId": "<providerId>",
  "dataDestination": {
    "type": "HttpProxy"
  },
  "createdAt": 1688465655
}

```

The Transfer Process and also this tutorial as a whole was successful when `state == COMPLETED`.
