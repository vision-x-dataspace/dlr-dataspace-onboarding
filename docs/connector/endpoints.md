# Endpoints

## Connector

The `Connector API` is available under `/connectors` and has the following endpoints. Most endpoints require a bearer token to be passed as a header along with the request.

| Endpoint                            | Type   | Description                                      |
|-------------------------------------|--------|--------------------------------------------------|
| **/**                               | GET    | Gets all Connectors for the given user           |
| **/&lt;name&gt;**                   | POST   | Creates a Connector given some configuration     |
| **/&lt;name&gt;**                   | DELETE | Deletes the Connector with name '&lt;name&gt;'   |
| **/&lt;name&gt;**                   | GET    | Gets the Connector with name '&lt;name&gt;'      |
| **/&lt;name&gt;**                   | POST   | Creates a Connector given some settings          |
| **/&lt;name&gt;**                   | PUT    | Edits the Connector with name '&lt;name&gt;'     |
| **/&lt;name&gt;/start**             | GET    | Starts the Connector with name '&lt;name&gt;'    |
| **/&lt;name&gt;/stop**              | GET    | Stops the Connector with name '&lt;name&gt;'     |
| **/&lt;name&gt;/logs/controlplane** | GET    | Gets the logs of the Connector's Controlplane    |
| **/&lt;name&gt;/logs/dataplane**    | GET    | Gets the logs of the Connector's Dataplane       |
| **/&lt;name&gt;/dsp/.\***           | \*     | Reroutes to the DSP API of the Connnector        |
| **/&lt;name&gt;/health/.\***        | \*     | Reroutes to the Health API of the Connnector     |
| **/&lt;name&gt;/management/.\***    | \*     | Reroutes to the Management API of the Connnector |
| **/&lt;name&gt;/proxy/.\***         | \*     | Reroutes to the Proxy API of the Connnector      |
| **/&lt;name&gt;/public/.\***        | \*     | Reroutes to the Public API of the Connnector     |
| **/&lt;name&gt;/vault/.\***         | \*     | Reroutes to the API for the Connnector' Vault    |

## DSP

The `DSP API` is available under `/dsp` and has the following endpoints.

| Endpoint                            | Type   | Description                                      |
|-------------------------------------|--------|--------------------------------------------------|
| **/**                               | GET    | Gets the DSP endpoints of all running Connectors |

## Token

The `Token API` is available under `/token` and has the following endpoints.

| Endpoint                            | Type   | Description                                      |
|-------------------------------------|--------|--------------------------------------------------|
| **/**                               | POST   | Gets a JWT from Keycloak                         |
