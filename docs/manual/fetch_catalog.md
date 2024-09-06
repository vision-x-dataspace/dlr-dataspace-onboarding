# Fetching the Federated Catalog

## Introduction

The federated catalog API is the first request in this sequence that passes through the Dataspace. It is executed by the Data Consumer against their own Control Plane and shows the catalog of all other participants which are periodically retrieved. The request
looks like this:

## Request

```http
POST /federatedcatalog HTTP/1.1
Host: http://vision-x-dataspace.base-x-ecosystem.org/<your-connector-name>/management
X-Api-Key: <your-password>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-password>` with your password.

```json
{}
```

The returned payload is a list of `dcat:Catalog`. The `Catalogs` may look something like this.

```json
{
  "@id": "10b1b0f3-5a67-4eee-9404-5a300356a50d",
  "@type": "dcat:Catalog",
  "dcat:dataset": [
    {
      "@id": "<asset-id>",
      "@type": "dcat:Dataset",
      "odrl:hasPolicy": {
        "@id": "Y29udHJhY3QtZ2V0LTE=:anNvbi1nZXQtMQ==:MDEwODg2ZTItZDhmNi00Y2NjLWFhMWYtY2U2Y2JmYjlmMWQz",
        "@type": "odrl:Set",
        "odrl:permission": {
          "odrl:target": "<asset-id>",
          "odrl:action": {
            "odrl:type": "http://www.w3.org/ns/odrl/2/use"
          },
          "odrl:constraint": {
            "odrl:leftOperand": "https://w3id.org/tractusx/v0.0.1/ns/Membership",
            "odrl:operator": {
              "@id": "odrl:eq"
            },
            "odrl:rightOperand": "active"
          }
        },
        "odrl:prohibition": [],
        "odrl:obligation": [],
        "odrl:target": "<asset-id>"
      },
      "dcat:distribution": [
        {
          "@type": "dcat:Distribution",
          "dct:format": {
            "@id": "HttpProxy"
          },
          "dcat:accessService": "b4f2c6b6-d3d1-46e2-a517-6912b7f8a509"
        },
        {
          "@type": "dcat:Distribution",
          "dct:format": {
            "@id": "AmazonS3"
          },
          "dcat:accessService": "b4f2c6b6-d3d1-46e2-a517-6912b7f8a509"
        }
      ],
      "description": "Json Get Asset",
      "id": "<asset-id>",
      "dct:type": {
        "@id": "https://my-namespa.ce/my-asset-type"
      }
    }
  ],
  "dcat:service": {
    "@id": "b4f2c6b6-d3d1-46e2-a517-6912b7f8a509",
    "@type": "dcat:DataService",
    "dct:terms": "connector",
    "dct:endpointUrl": "https://<provider-control>/api/v1/dsp"
  },
  "participantId": "<prodvider-bpn>",
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/",
    "dct": "https://purl.org/dc/terms/",
    "tx": "https://w3id.org/tractusx/v0.0.1/ns/",
    "edc": "https://w3id.org/edc/v0.0.1/ns/",
    "dcat": "https://www.w3.org/ns/dcat/",
    "odrl": "http://www.w3.org/ns/odrl/2/",
    "dspace": "https://w3id.org/dspace/v0.8/"
  }
}
```

Find the offer for your chosen `<asset-id>` and note down all of `odrl:hasPolicy` as well as `dcat:service.dct:endpointUrl` and `participantId` for the next step.

## Explanation

In the catalog above, some properties are meta-data that's independent of whether the Provider extends any Data Offers to the Consumer.

- The `@id` is the identifier for this catalog. As the catalog is created dynamically, the id is a UUID regenerated for each request to the Provider's catalog.
- `dcat:service` holds data about the Provider's connector that the Consumer's connector communicated with. Especially the `dcat:endpointUrl` will become important in the next step.
- `participantId` signifies the BPN of the Provider. This is specific to the EDC and not mandated by the DSP-spec.

The Data Offers are hidden in the `dcat:dataset` section, grouped by the Asset that the offer is made for. Consequently, if there may be more than one offer for the same Asset, requiring a Data Consumer to select based on the policies included.

- The `@id` corresponds to the id of the Asset that can be negotiated for.
- `dcat:Distribution` makes statements over which Data Planes an Asset's data can be retrieved.
- `dcat:hasPolicy` holds the Data Offer that is relevant for the Consumer.
    - `@id` is the identifier for the Data Offer. The EDC composes this id by concatenating three identifiers in base64-encoding separated with `:` (colons). The format is `base64(contractDefinitionId):base64(assetId):base64(newUuidV4)`. The last of three UUIDs changes with every request as every /v2/catalog/request call yields a new catalog with new Data Offers.
    - The `odrl:target` properties in the Data Offer always hold the Asset's id.
    - The `odrl:permission`, `odrl:prohibition` and `odrl:obligation` will hold the content of the contractPolicy configured in the Contract Definition the Contract Offer was derived from.

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/04_catalog.md).
