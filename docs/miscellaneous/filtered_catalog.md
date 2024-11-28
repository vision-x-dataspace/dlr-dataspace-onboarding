# Filtered Catalog

## Single Catalog

To get the contents of the catalog of a single connector you can send the following request.

```http
POST /v2/catalog/request HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/alice/management
Authorization: Bearer <token-alice>
Content-Type: application/json
```

```json
{
  "@context": {},
  "counterPartyAddress": "https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/bob/dsp",
  "protocol": "dataspace-protocol-http",
  "querySpec": {
    "offset": 0,
    "limit": 50,
    "filterExpression": []
  }
}
```

One can also further filter this by adding to the 'filterExpression' list. For example
```json
{
  "operandLeft": "https://w3id.org/edc/v0.0.1/ns/id",
  "operator": "like",
  "operandRight": "test-asset-%"
}
```
This filters for all assets whose 'id' start with 'test-asset-'

## Single Dataset

To get a single dataset from a catalog you can send the following request.

```http
POST /v2/catalog/dataset/request HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/alice/management
Authorization: Bearer <token-alice>
Content-Type: application/json
```

```json
{
  "@context": {},
  "@id": "asset-1",
  "counterPartyAddress": "https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/bob/dsp",
  "protocol": "dataspace-protocol-http"
}
```

This will only get the dataset with id 'asset-1' and as such has the same effect as using
```json
{
  "operandLeft": "https://w3id.org/edc/v0.0.1/ns/id",
  "operator": "=",
  "operandRight": "asset-1"
}
```
as 'filterExpression' in the 'Single Catalog' section.
