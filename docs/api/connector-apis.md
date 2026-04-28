# Connector APIs

The connector consists of several software components, each exposing a number of APIs. Please refer to other parts of this documentation for more information on the components in general.

## Controlplane

=== "Management API"

    The **Management API** lets you manage all your **Assets**, **Policy Definitions**, and more.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/cp/management` |
    | Access   | Protected |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [Management API docs](https://eclipse-edc.github.io/Connector/openapi/management-api/).

=== "Protocol API"

    The **Protocol API** enables communication between connectors and is only meant to be used directly by connectors themselves.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/cp/protocol` |
    | Access   | Public |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [DSP API docs](https://eclipse-edc.github.io/Connector/openapi/dsp-api/).

=== "Default API"

    The **Default API** exposes endpoints for checking health, readiness, and similar status indicators.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/cp/api` |
    | Access   | Public |

    !!! info "API Reference"
        Full documentation is available at the [Observability API docs](https://github.com/eclipse-edc /Connector/tree/main/extensions/common/api/api-observability/).

## Dataplane

=== "Public API"

    The **Public API** is used to perform **PULL** transfers.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/dp/public` |
    | Access   | Public |

    !!! info "API Reference"
        For more information, see [Public API](https://eclipse-edc.github.io/Connector/openapi/public-api/).

=== "Proxy API"

    The `Proxy API` is an alternative way to perform `PULL` transfers.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/dp/proxy` |
    | Access   | Protected |

    !!! info "API Reference"
        For more information, see [Proxy Consumer API](https://github.com/eclipse-tractusx/tractusx-edc/tree/main/edc-extensions/dataplane/dataplane-proxy/edc-dataplane-proxy-consumer-api).

## Identity Hub

=== "Identity API"

    The **Identity API** is used to manage your **DID Documents**, **Verifiable Credentials**, and more.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/ih/identity` |
    | Access   | Protected |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [Identity API docs](https://eclipse-edc.github.io/IdentityHub/openapi/identity-api/).

=== "Presentation API"

    The **Presentation API** allows clients to request credentials in the form of a **Verifiable Presentation**.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/ih/presentation` |
    | Access   | Public |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [Presentation API docs](https://eclipse-edc.github.io/IdentityHub/openapi/presentation-api/).

=== "STS API"

    The **STS API** is responsible for generating **ID-Tokens** to access the **Presentation API**.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/connectors/<connector-name>/ih/sts` |
    | Access   | Protected |

    !!! info
        For more information, see [Identity Hub STS](https://github.com/eclipse-edc/IdentityHub/tree/main/extensions/sts).

## DID Document

The **DID Document** of a connector can be viewed by sending a request to its dedicated endpoint.

```http
GET /connector/<connector-name>/did.json
```

## Vault Token

The vault token to access the [Hashicorp Vault](https://vision-x-vault.base-x-ecosystem.org) can be retrieved as follows.

```http
GET /connectors/<connector-name>/vault/token
```

!!! tip
    The given information allows you to put secrets into the vault yourself that your connector is able to retrieve.

## Code Examples

=== "Create Asset"

    === "curl"

        ```bash
        curl -X POST https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/management/v3/assets \
          -H "Authorization: Bearer sk-..." \
          -H "Content-Type: application/json" \
          -d '{
            "@context": {
              "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
            },
            "@type": "Asset",
            "@id": "my-asset-id",
            "properties": {
              "name": "My Asset",
              "description": "A sample asset"
            },
            "dataAddress": {
              "@type": "DataAddress",
              "type": "HttpData",
              "baseUrl": "https://example.com/data"
            }
          }'
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/management/v3/assets"
        headers = {
            "Authorization": "Bearer sk-...",
            "Content-Type": "application/json",
        }
        payload = {
            "@context": {
                "@vocab": "https://w3id.org/edc/v0.0.1/ns/"
            },
            "@type": "Asset",
            "@id": "my-asset-id",
            "properties": {
                "name": "My Asset",
                "description": "A sample asset",
            },
            "dataAddress": {
                "@type": "DataAddress",
                "type": "HttpData",
                "baseUrl": "https://example.com/data",
            },
        }

        response = requests.post(url, json=payload, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```

=== "Start Negotiation"

    === "curl"

        ```bash
        curl -X POST https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/management/v3/contractnegotiations \
          -H "Authorization: Bearer sk-..." \
          -H "Content-Type: application/json" \
          -d '{
            "@context": {
              "@vocab": "https://w3id.org/edc/v0.0.1/ns/",
              "odrl": "http://www.w3.org/ns/odrl/2/"
            },
            "@type": "ContractRequest",
            "counterPartyAddress": "https://provider.example.com/cp/protocol",
            "protocol": "dataspace-protocol-http",
            "policy": {
              "@type": "Offer",
              "@id": "Y29udHJhY3QtZGlkOmFzc2V0LWlkOjU1MGU4NDAwLWUyOWItNDFkNC1hNzE2LTQ0NjY1NTQ0MDAwMA==",
              "odrl:assigner": {"@id": "BPNL0123456789AB"},
              "odrl:target": {"@id": "asset-id"}}
            }
          }'
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/management/v3/contractnegotiations"
        headers = {
            "Authorization": "Bearer sk-...",
            "Content-Type": "application/json",
        }
        payload = {
            "@context": {
                "@vocab": "https://w3id.org/edc/v0.0.1/ns/",
                "odrl": "http://www.w3.org/ns/odrl/2/"
            },
            "@type": "ContractRequest",
            "counterPartyAddress": "https://provider.example.com/cp/protocol",
            "protocol": "dataspace-protocol-http",
            "policy": {
                "@type": "Offer",
                "@id": "Y29udHJhY3QtZGlkOmFzc2V0LWlkOjU1MGU4NDAwLWUyOWItNDFkNC1hNzE2LTQ0NjY1NTQ0MDAwMA==",
                "odrl:assigner": {"@id": "BPNL0123456789AB"},
                "odrl:target": {"@id": "asset-id"}}
            },
        }

        response = requests.post(url, json=payload, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```

=== "Check Health"

    === "curl"

        ```bash
        curl -X GET https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/api/check/health \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/cp/api/check/health"

        response = requests.get(url)
        response.raise_for_status()
        print(response.json())
        ```

=== "Pull EDR"

    === "curl"

        ```bash
        curl -X GET https://vision-x-api.base-x-ecosystem.org/connectors/alice/dp/public \
          -H "Authorization: Bearer eyJ..." \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/dp/public"
        headers = {"Authorization": "Bearer eyJ..."}

        response = requests.get(url, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```

=== "Get Credentials"

    === "curl"

        ```bash
        curl -X GET https://vision-x-api.base-x-ecosystem.org/connectors/alice/ih/identity/v1alpha/participants/YWxpY2U=/credentials \
          -H "Authorization: Bearer sk-..." \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/connectors/alice/ih/identity/v1alpha/participants/YWxpY2U=/credentials"
        headers = {
            "Authorization": "Bearer sk-...",
            "Accept": "application/json",
        }

        response = requests.get(url, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```
