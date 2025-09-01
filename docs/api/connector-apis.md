# Connector APIs

The Connector consists of several software components. Each of these expose several APIs. Please refer to other parts of this documentation, for more information on the components in general.

## Controlplane

### Management API

The `Management API` lets you manage all your `Assets`, `Policy Definitions`, etc. It is available at `/connectors/<connector-name>/cp/management` and all of its endpoints are protected. For detailled documentation on this API, see [Tractus-X EDC control-plane API](https://eclipse-tractusx.github.io/tractusx-edc/openapi/control-plane-api/). Note that the section "Application Observability" in the Tractus-X EDC documentation is not part of the `Management API` but part of the `Default API` instead.


## Protocol API

The `Protocol API` enables communication between Connectors and only meant to be used directly by Connectors themselves. It is available at `/connectors/<connector-name>/cp/protocol`. For detailled documentation on this API, see [EDC dsp-api](https://eclipse-edc.github.io/Connector/openapi/dsp-api/).

## Default API

The `Default API` exposes endpoints for checking health, readiness and simlar status indicators. It is available at `/connectors/<connector-name>/cp/default`. For detailled documentation on this API, see [Tractus-X EDC control-plane API](https://eclipse-tractusx.github.io/tractusx-edc/openapi/control-plane-api/), specifically the "Application Observability" section.

## Dataplane

### Public API

The `Public API` is used to perform `PULL` transfers. It is available at `/connectors/<connector-name>/dp/public`. For an example on how to utilize this API, see [Tractus-X EDC Walkthrough](https://github.com/eclipse-tractusx/tractusx-edc/blob/0.9.0/docs/usage/management-api-walkthrough/07_edrs.md).

### Proxy API

The `Proxy API` can also alternatively be used for `PULL` transfers. It is available at `/connectors/<connector-name>/dp/proxy` and all of its endpoints are protected. For an example on how to utilize this API, see [Tractus-X EDC Walkthrough](https://github.com/eclipse-tractusx/tractusx-edc/blob/0.9.0/docs/usage/management-api-walkthrough/07_edrs.md).

## Default API

The `Default API` exposes endpoints for checking health, readiness and simlar status indicators. It is available at `/connectors/<connector-name>/dp/default`. For detailled documentation on this API, see [Tractus-X EDC data-plane API](https://eclipse-tractusx.github.io/tractusx-edc/openapi/data-plane-api/), specifically the "Application Observability" section.

## Identity Hub

### Identity API

The `Identity API` is used to manage your `DID documents`, `Verifiably Credentials`, etc. It is available at `/connectors/<connector-name>/ih/identity` and all of its endpoints are protected. For detailled documentation on this API, see [IdentityHub identity-api](https://eclipse-edc.github.io/IdentityHub/openapi/identity-api/).

### Presentation API

The `Presentation API` allows clients to request credentials in the form of a `Verifiable Presentation`. It is available at `/connectors/<connector-name>/ih/presentation`. For detailled documentation on this API, see [IdentityHub presentation-api](https://eclipse-edc.github.io/IdentityHub/openapi/presentation-api/).

### STS API

The `STS API` is responsible for generating `ID-Tokens` to access the `Presentation API`. It is available at `/connectors/<connector-name>/ih/sts` and all of its endpoints are protected. As it is only supposed to be used internally, this documentation will not provide a detailled description.

## Default API

The `Default API` exposes endpoints for checking health, readiness and simlar status indicators. It is available at `/connectors/<connector-name>/ih/default`. It works exactly the same as for the control and data plane.

## DID Document

The `DID Document` can of a Connector viewed by sending a `GET` request to `/connector/<connector-name>/did.json`.

## Vault Token

The vault token to access the `Hashicorp Vault` at [vision-x-vault.base-x-ecosystem.org](https://vision-x-vault.base-x-ecosystem.org) can be retrieved by making a `GET` request to `/connectors/<connector-name>/vault/token`. The vault can be used to provide the Connector with confidential information thourgh there rather than sending them directly in requests to the Connector.
