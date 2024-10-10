# Failed Negotiations and Transfers

It can happen that a negotiation or transfer fails transition to the 'FINALIZED' or 'COMPLETED' state. Instead the state might transition to 'TERMINATED' or get stuck at 'REQUESTED' and so on.

In these cases there is no easy way to get information on what exactly went wrong without directly looking at the logs of the connector. But for almost all of these cases the reason for failing is a wrong input parameter in the initiation request.

Some common examples for the negotiation include

- the 'connectorAddress' was not set correctly
- the 'policy' was not successfully copied from the corresponding offer in the catalog

Some common examples for the transfer include

- the 'connectorAddress' was not set correctly
- the 'contractAgreementId' was not set correctly
- the 'dataDestination' points to a file that does not exist or includes a wrong storage address or credentials
