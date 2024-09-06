# Creating a Contract Definition

## Introduction

A Contract Definition is the connection between a set of Assets with one Access Policy and one Contract Policy. The two policies are both policies as explained previously but checked in different stages of communication between Data Provider and Data Consumer. The creation request looks like this:

## Request

```http
POST /v2/contractdefinitions HTTP/1.1
Host: https:/vision-x-dataspace.base-x-ecosystem.org/<your-connector-name>/management
X-Api-Key: <your-password>
Content-Type: application/json
```

```json
{
  "@context": {
    "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
  },
  "@type": "ContractDefinition",
  "@id": "<contract-id>",
  "accessPolicyId": "<policy-id>",
  "contractPolicyId": "<policy-id",
  "assetsSelector": 
    {
      "operandLeft": "https://w3id.org/edc/v0.0.1/ns/id",
      "operator": "=",
      "operandRight": "<asset-id>"
    }
  
}
```

Replace `<contract-id>` by some ID of your choice and replace `<asset-id>` and `<policy-id>` by the values chosen in the previous steps.

## Explanation

`accessPolicyId` and `contractPolicyId` are the identifiers of the policies used in the contract definition. On creation, the EDC does not automatically check if a policy with the corresponding `@id` exists - the call sequence will fail later when the Data Consumer attempts to find the offer in the catalog-request.

The `assetsSelector` is an EDC-Criterion. This class specifies filters over a set of objects, Assets in this case. The concept is functionally similar to the `odrl:Constraint` in a Policy but syntactically different.
- `operandLeft` is a property in the Entity (`Asset` in this case) that is assigned a value.
- `operator` is the logical operation that will be used to compare the `operandLeft` with the `operandRight`.
- `operandRight` is the constant that the dynamically retrieved value of `operandLeft` will be compared to via the `operator`.

This mechanism allows the administrator to bind the same policies to multiple assets. The example on the top of this page will only match a single Asset as the `id` will be unique as it's derived from the Asset's `@id`. It is however possible to match multiple Assets if they share a common property:

```json
{
  "assetsSelector": {
    "operandLeft": "https://w3id.org/edc/v0.0.1/ns/myCommonProperty",
    "operator": "=",
    "operandRight": "sharedValue"
  }
}
```

For more detailed information see [here](https://github.com/eclipse-tractusx/tractusx-edc/blob/release/0.6.0/docs/usage/management-api-walkthrough/03_contractdefinitions.md).
