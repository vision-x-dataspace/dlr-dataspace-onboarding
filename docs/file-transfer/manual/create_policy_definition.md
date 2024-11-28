# Creating a Policy Definition

## Introduction

A policy is a declaration of a Data Consumer's rights and duties. Policies themselves make no statements about the object that they may grant access and usage permission to. They are created at the EDC like this:

## Request

```http
POST /v2/policydefinitions HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/connectors/<your-connector-name>/management
Authorization: Bearer <your-token>
Content-Type: application/json
```

Replace `<your-connector-name>` with the actual name of the connector assigned to you and `<your-token>` with your token.

```json
{
  "@context": {
    "odrl": "http://www.w3.org/ns/odrl/2/"
  },
  "@type": "PolicyDefinitionRequestDto",
  "@id": "<policy-id>",
  "policy": {
    "@type": "Policy",
    "odrl:permission": [
      {
        "odrl:action": "use",
        "odrl:constraint": {
          "@type": "Constraint",
          "odrl:leftOperand": "BusinessPartnerNumber",
          "odrl:operator": {
            "@id": "odrl:eq"
          },
          "odrl:rightOperand": "<BPN_CONSUMER>"
        }
      }
    ]
  }
}

```

Replace `<policy-id>` by some ID of your choice.

## Explanation

In the EDC, policies are pure [ODRL (Open Digital Rights Language)](https://www.w3.org/TR/odrl-model/) written in JSON-LD.

Even if the user only has rudimentary knowledge of JSON-LD, the [policy playground](https://eclipse-tractusx.github.io/tutorial-resources/policy-playground/) will provide a good starting point to start writing policies.

It is important to keep in mind that the extensive ODRL-context (that the EDC is aware of) allows for ergonomic reuse of the vocabulary in individual policies.

### Writing Policies for the EDC

ODRL's model and expressiveness surpass the EDC's current ability to interpret the policies and derive behavior from them. This must be kept in mind even when Data Offers based on policies are not yet published to the Dataspace. Here again, configuring the wrong policies is a risk for unsafe and non-compliant behavior. This is exacerbated by the fact that the EDC interprets policies it can't evaluate as true by default. A couple of examples:

### Let all pass

```json
{
  "@context": {
    "odrl": "http://www.w3.org/ns/odrl/2/"
  },
  "@type": "PolicyDefinitionRequest",
  "@id": "{% uuid 'v4' %}",
  "policy": {
    "@type": "Policy",
    "odrl:permission": [
      {
        "odrl:action": "use"
      }
    ]
  }
}
```

### Only let a Business Partner Group pass

A Business Partner Group is a group of BPNs that are allowed to pass this constraint. A BPN can be added to a group even after a Contract Offer for a certain BPN-Group was published. The groups are persisted and maintained in the Provider's Control Plane. The EDC-Management-API's `/business-partner-groups` endpoint offers CRUD-operations for
it.

```json
{
  "@context": {
    "tx": "https://w3id.org/tractusx/v0.0.1/ns/"
  },
  "@type": "PolicyDefinitionRequest",
  "@id": "{% uuid 'v4' %}",
  "policy": {
    "@type": "Set",
    "@context": "http://www.w3.org/ns/odrl.jsonld",
    "permission": [
      {
        "action": "use",
        "constraint": [
          {
            "leftOperand": "tx:BusinessPartnerGroup",
            "operator": "isPartOf",
            "rightOperand": "<group>"
          }
        ]
      }
    ]
  }
}

```

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/02_policies.md).
