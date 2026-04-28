# Getting Started

## General Information

The API is hosted at [vision-x-dataspace.base-x-ecosystem.org](https://vision-x-api.base-x-ecosystem.org). An OpenAPI spec is available [here](https://vision-x-api.base-x-ecosystem.org/docs).

!!! note "Authorization"
    To use most API endpoints you need to provide a bearer token e.g. an API key in the `Authorization` header of your requests.

## Get your API Key

1. Sign in at [vision-x-dataspace.base-x-ecosystem.org](https://vision-x-dataspace.base-x-ecosystem.org)
2. Generate an API key using the button in the upper right corner
3. Copy and save the generated API key somewhere safe

!!! warning "Key Visibility"
    The full API key is only shown **once** upon generation. Make sure to copy and store it immediately.

Once you have your key, include it in the header of requests.

```http
Authorization: Bearer sk-...
```

!!! info "Revocation"
    Generating a new API key **revokes all previous ones**. API keys have no expiration date.
