# Federated

There are a number of endpoints which can be used to retrieve aggregate information on all users overall.

!!! info "Note"
    For efficiency purposes these endpoints use caching. Thus, information might ocassionally be slightly out of sync.

## Endpoints

=== "User"
    Retrieve a mapping of users to the list of BPNs of their Connectors.

    `GET /federated/user`

=== "Group"
    Retrieve a mapping of groups to the list of users in it.

    `GET /federated/group`

=== "DID"
    Retrieve a list of DIDs of all running Connectors.

    `GET /federated/did`

=== "BPN"
    Retrieve a mapping of Connector BPNs to their user.

    `GET /federated/bpn`

=== "Catalog"
    Retrieve a collection of all offers of all running connectors.

    `GET /federated/catalog`

    !!! info "Group filtering"
        One can optionally filter to only get the offers of users in a specified group.

## Catalog (POST)

In addition to the regular catalog endpoint one can also formulate more specific criteria at this endpoint.

```http
POST /federated/catalog/query
```

!!! info "API Reference"
    For more information on this, see [Federated Catalog catalog-api](https://eclipse-edc.github.io/FederatedCatalog/openapi/catalog-api/#/Federated%20Catalog/getCachedCatalog).

## Code Examples

=== "Get Users"

    === "curl"

        ```bash
        curl -X GET "https://vision-x-api.base-x-ecosystem.org/federated/user" \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/federated/user"

        response = requests.get(url)
        response.raise_for_status()
        print(response.json())
        ```

=== "Get Catalog"

    === "curl"

        ```bash
        curl -X GET "https://vision-x-api.base-x-ecosystem.org/federated/catalog" \
          -H "Accept: application/json"
        ```

    === "Python"

        ```python
        import requests

        url = "https://vision-x-api.base-x-ecosystem.org/federated/catalog"

        response = requests.get(url)
        response.raise_for_status()
        print(response.json())
        ```
