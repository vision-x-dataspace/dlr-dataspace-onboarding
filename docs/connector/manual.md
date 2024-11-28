# Manual

## Get Token

First you need to get a token with your credentials. You can do so by sending the following request.

```http
POST /token HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/
Content-Type: application/json
```

```json
{
    "username": "<your-username>", 
    "password": "<your-password>"
}
```

You should receive a response containing an "access_token". This is the token that you will have to use for the following requests


## Create Connector

This request will create a `Connector`. It will take a will until it is running.

```http
POST /connectors/<your-connector-name> HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/
Authorization: Bearer <your-token>
Content-Type: application/json
```

Replace `<your-connector-name>` with the name that you want to give to the `Connector` and `<your-token>` with your token.

```json
{}
```

## Get Connector

With this request you can check the current status of the `Connector`.

```http
GET /connectors/<your-connector-name> HTTP/1.1
Host: https://vision-x-dataspace.base-x-ecosystem.org/backend/
Authorization: Bearer <your-token>
Content-Type: application/json
```

Replace `<your-connector-name>` with the name that you want to give to the `Connector` and `<your-token>` with your token.

## More

For information on other endpoints check out the other sections.
