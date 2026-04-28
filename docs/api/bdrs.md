# BDRS

The **BDRS** ([BPN-DID Resolution Service](https://github.com/eclipse-tractusx/bpn-did-resolution-service)) provides a mapping between **BPNs** (Business Partner Numbers) and **DIDs** (Decentralized Identifiers).

!!! warning "Connector Configuration"
    Each connector is configured ot use this BDRS for DID resolution. Thus, making the issuer a quasi-central component of the dataspace.

!!! note "DSP 2025"
    For communication via [DSP 2025](https://github.com/eclipse-edc/Connector/tree/main/data-protocols/dsp/dsp-2025) the BDRS is no longer strictly necessary.

## APIs

=== "Management API"

    The **Management API** is used to create and manage BPN–DID mappings.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/bdrs/management` |
    | Access   | Administrators only |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [Management API docs](https://eclipse-tractusx.github.io/bpn-did-resolution-service/openapi/management-api/).

=== "Directory API"

    The **Directory API** allows you to retrieve existing BPN–DID mappings.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/bdrs/directory` |
    | Access   | Public |

    !!! info "API Reference"
        Full OpenAPI documentation is available at the [Directory API docs](https://eclipse-tractusx.github.io/bpn-did-resolution-service/openapi/directory-api/).

## Code Examples

=== "Add BPN-DID Entry"

    === "curl"

        ```bash
        curl -X POST https://vision-x-api.base-x-ecosystem.org/bdrs/management/bpn-directory \
          -H "Authorization: Bearer sk-..." \
          -H "Content-Type: application/json" \
          -d '{
            "bpn": "BPNL000000000001",
            "did": "did:web:example.com:BPNL000000000001"
          }'
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/bdrs/management/bpn-directory"
        headers = {
            "Authorization": "Bearer sk-...",
            "Content-Type": "application/json",
        }
        payload = {
            "bpn": "BPNL000000000001",
            "did": "did:web:example.com:BPNL000000000001",
        }

        response = requests.post(url, json=payload, headers=headers)
        response.raise_for_status()
        print(response.json())
        ```

=== "Retrieve Full Mapping"

    === "curl"

        ```bash
        curl -X GET "https://vision-x-api.base-x-ecosystem.org/bdrs/directory" \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/bdrs/directory/bpn-directory"

        response = requests.get(url)
        response.raise_for_status()
        print(response.json())
        ```
