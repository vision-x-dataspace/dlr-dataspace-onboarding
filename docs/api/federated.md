# Federated

There are a number of endpoints which can be used to retrieve aggregate information on all users overall.

## User

A mapping of users to the list of `BPNs` of their Connectors can be retrieved by sending a `GET` request to `/federated/user`.

## Group

A mapping of groups to the list of users in it can be retrieved by sending a `GET` request to `/federated/group`.

## DID

A list of the `DIDs` of all running Connectors can be retrieved by sending a `GET` request to `/federated/did`.

## BPN

A mapping of Connector `BPNs` to their user can be retrieved by sending a `GET` request to `/federated/bpn`.

## Catalog

A collection of all offers of all running Connectors, the `Federated Catalog`, can be retrieved by sending a `GET` request to `/federated/catalog`. One can optionally specify a "group" argument to only get the offers of users in the specified group.

## Catalog (POST)

In addition to the regular catalog endpoint one can also send a `POST` request to `/federated/catalog/query` to formulate more specific criteria. For more information on this, see [Federated Catalog catalog-api](https://eclipse-edc.github.io/FederatedCatalog/openapi/catalog-api/#/Federated%20Catalog/getCachedCatalog).
