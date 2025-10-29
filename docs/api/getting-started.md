# Getting started

To use most API endpoints you need to provide a bearer token ([JWT](https://de.wikipedia.org/wiki/JSON_Web_Token)) in the `Authorization` header of you requests. This token can be aquired from [Keycloak](https://github.com/keycloak/keycloak) running on [vision-x-auth.base-x-ecosystem.org](https://vision-x-auth.base-x-ecosystem.org).

## Get your Certificate

1. Sign in at [vision-x-dataspace.base-x-ecosystem.org](https://vision-x-dataspace.base-x-ecosystem.org)
2. Download the `cert.zip` file by clicking on the download button in the upper right corner
3. Unzip the file and store the contained files (tls.crt, tls.key and cert.p12) somewhere on your device

## Get a Bearer Token

Now you can get the token by sending a request to the [Token Endpoint](https://vision-x-auth.base-x-ecosystem.org/realms/user/protocol/openid-connect/token) of [Keycloak](https://github.com/keycloak/keycloak) using the certificate files. Concrete instructions on how to do this with several tools are [further below](#example-requests).

The response should look something like this
```json
{
  "access_token": "ey...",
  "expires_in": 28800,
  "refresh_expires_in": 0,
  "token_type": "Bearer",
  "id_token": "ey...",
  "not-before-policy": 0,
  "scope": "openid profile email"
}
```

For most API requests, you must include the `access_token` in the `Authorization` header using the format: `Authorization: Bearer <your-access-token>`. Such endpoints will hereafter be referred to as 'protected'.

Note that this token is valid for 8 hours, after which you will need to send another request to get a new one.

## Example requests

Here are a concrete examples on how to use the certificate files to send the request to get the token.

### curl

```bash
curl -k --cert <cert-files-dir>/tls.crt --key <cert-files-dir>/tls.key \
  -X POST "https://vision-x-auth.base-x-ecosystem.org/realms/user/protocol/openid-connect/token" \
  -d "client_id=client-<your-username>" \
  -d "grant_type=client_credentials" \
  -d "scope=openid"
```

### python

```python
from pathlib import Path
import requests

username = "<your-username>"

cert_files_dir = Path("<cert-files-dir>")
cert = (cert_files_dir / "tls.crt", cert_files_dir / "tls.key")

url = "https://vision-x-auth.base-x-ecosystem.org/realms/user/protocol/openid-connect/token"
data = {
    "client_id": f"client-{username}",
    "grant_type": "client_credentials",
    "scope": "openid"
}

response = requests.post(url, data=data, cert=cert)

print(response.json())
```
