# Issuer

The **issuer** is responsible for issuing **Verifiable Credentials**.

!!! warning "Trusted Issuers"
    Each connector is configured with this issuer as its only trusted issuer. As such an VCs issued by other issuers will not be trusted. Thus, making the issuer a quasi-central component of the dataspace.

## Endpoints

=== "Issue"

    Credentials can be issued by sending a request to these endpoints respectively.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/issuer/issue/membership` |
    | Endpoint | `/issuer/issue/bpn` |
    | Endpoint | `/issuer/issue/governance` |
    | Access   | Administrators only |

    !!! info "Request Details"
        As these endpoints are protected and can only be used by administrators, this documentation will provide no detailled explanation on them.

=== "DID Document"

    The **DID Document** can of the issuer be viewed at the following endpoint.

    | Property | Value |
    |----------|-------|
    | Endpoint | `/issuer/did.json` |
    | Access   | Public |

    !!! info "DID"
        For more information on DIDs, see [Decentralized Identifiers](https://www.w3.org/TR/did-1.0/).

## Code Examples

=== "Issue BPN credential"

    === "curl"

        ```bash
        curl -X POST https://vision-x-api.base-x-ecosystem.org/issuer/issue/bpn \
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

        url = "https://vision-x-api.base-x-ecosystem.org/issuer/issue/bpn"
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

=== "Retrieve DID document"

    === "curl"

        ```bash
        curl -X GET "https://vision-x-api.base-x-ecosystem.org/issuer/did.json" \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/issuer/did.json"

        response = requests.get(url)
        response.raise_for_status()
        print(response.json())
        ```
