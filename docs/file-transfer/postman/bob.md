## Introduction

In this part you will negotiate a `Contract Agreement` for the `Offer` created in the previous part and perform a `Transfer Process` for the `Offer`.

## Fetch Catalog

The first step is to fetch the `Federated Catalog` containing all `Offers` of all `Participants` of the `Dataspace`.

The `Federated Catalog` is unique to each `Participant` and periodically updated by querying all other `Connectors` for their `Catalog`. This means that if ones own `Connector` does not satisfy the `Access Policy` of a `Contract Definition`, then no `Offers` will be generated for this `Contract Definition` and as such no `Offers` will be visible in ones `Federated Catalog`.

## Initiate Negotation

The second step is to take the `participantId` and `originator` of the `Catalog` where the desired `Offer` is located in as well as the whole `odrl:hasPolicy` of the `Offer` and use them to initiate a `Contract Negotiation` with the `Participant` providing the `Offer`.

These values are automatically retrieved and stored as variables in the `Postman Collection`.

## Get Negotiation

The next step is to get the `ID` of the `Contract Agreement` which is generated when a `Contract Negotiation` proccessed and utlimately 'FINALIZED'.

This request should be sent at least a few seconds after the previous step, since it takes a bit for the `Contract Negotiation` to reach the point at which the `Contract Agreement` is generated.

The `ID` of the `Contract Agreement` is automatically retrieved and stored as variables in the `Postman Collection`.

# Initiate Transfer

In this step a `Transfer Process` is initiated in a similar way to the `Contract Negotiation` by additionally referencing the `Contract Agreement` by its `ID` and providing sufficient addresses and credentials for the `Connector` providing the `Offer` to put the file in some bucket of an `AmazonS3` storage.

The `ID` of the `Transfer Process` is automatically retrieved and stored as variables in the `Postman Collection`.

## Get transfer

In this last step the `Transfer Process` should already be in the state 'COMPLETED' an thus the file transfer successfully performed.

This request should be sent at least a few seconds after the previous step, since it takes a bit for the file to be transfered and therefore the `Transfer Process` to reach the 'COMPLETED' state.

This step serves merely as confirmation that the transfer was indeed successful.
