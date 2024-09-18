# Initiating a Contract Negotiation

## Introduction

Contract Negotiation is the second check a Data Consumer has to pass before getting access rights to a backend resource. It includes
- a check of the Consumer's VC against the Offer's `contractPolicy`.
- a check of the `contractPolicy` against the policy the Data Consumer signals in the negotiation request to.

## Request

```http
POST /v2/contractnegotiations HTTP/1.1
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
  "@type": "ContractRequest",
  "connectorAddress": "<dcat:service.dct:endpointUrl>",
  "protocol": "dataspace-protocol-http",
  "providerId": "<providerId>",
  "connectorId": "<providerId>", 
  "policy": <odrl:hasPolicy>
}

```

Replace the string surrounded by `<>` with the values received from the last step and note down the received `@id`.

## Explanation

- `connectorAddress` sets the coordinates for the connector that the Consumer-EDC shall negotiate with (Provider
  EDC).
  It will usually end on /api/v1/dsp
- `protocol` must be "dataspace-protocol-http"
- `providerId` is the Data Provider's BPN
- `connectorId` and `providerId` must both hold the correct BPN for the `connectorAddress`.

This call does not yet return a negotiation result but rather a server-side generated id for the contract negotiation in the `@id` property.

```json
{
	"@type": "IdResponse",
	"@id": "773b8795-45f2-4c57-a020-dc04e639baf3",
	"edc:createdAt": 1701289079455,
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

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/05_contractnegotiations.md).

## Checking for Completion

```http
GET /v2/contractnegotiation/<@id> HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/<your-connector-name>/management
X-Api-Key: <your-password>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-password>` with your password. Also, replace `<@id>` by the ID revieved from above.

The returned details for the negotiation should look something like this:

```json
{
  "@type": "ContractNegotiation",
  "@id": "50bf14b9-8f6e-4975-8ada-6f24379a58a2",
  "type": "CONSUMER",
  "protocol": "dataspace-protocol-http",
  "state": "VERIFIED",
  "counterPartyId": "<providerId>",
  "counterPartyAddress": "<dcat:service.dct:endpointUrl>",
  "contractAgreementId": "<contractNegotiationId>",
  "createdAt": 1701351116766,
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

The Contract Negotiation was successful when `state == FINALIZED`.

Note down the `contractAgreementId`. It will will be important for the next step.
