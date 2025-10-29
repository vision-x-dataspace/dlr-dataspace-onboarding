# Issuer

The Issuer is responsible for issuing `Verifiable Credentials` and verifying `Verifiably Presentations`.

## Issue Credentials

Credentials can be issued by sending a `POST` request to `/issuer/issue/membership`, `/issuer/issue/bpn` and `/issuer/issue/governance` respectively. As these endpoints are protected and can only be used by administrators, this documentation will provide no detailled explanation on these endpoints.

## DID Document

The `DID Document` can be viewed by sending a `GET` request to `/issuer/did.json`. It can be used to verify `Verifiable Credentials` that where issued by the Issuer.
