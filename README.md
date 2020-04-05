# terraform-aws-lambda-edge-azure-auth

>Terraform module for [nickshine/lambda-edge-azure-auth].

This terraform module pulls down the [nickshine/lambda-edge-azure-auth] pre-packaged lambda
function (using a [local-exec] provisioner with __curl__), generates the required `config.json`
file based on the configured input variables, zips and creates the lambda function in AWS.

Example generated `config.json`:

```json
{
  "AUTH_REQUEST": {
      "client_id": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxx",
      "redirect_uri": "http://localhost:1313/_callback",
      "response_type": "code",
      "response_mode": "query",
      "scope": "openid email profile"
  },
  "TOKEN_REQUEST": {
      "client_id": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxx",
      "grant_type": "authorization_code",
      "redirect_uri": "http://localhost:1313/_callback",
      "client_secret": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxx"
  },
  "DISTRIBUTION": "demo",
  "PRIVATE_KEY": "-----BEGIN RSA PRIVATE KEY-----\nxxxxxxxxxx\n-----END RSA PRIVATE KEY-----\n",
  "PUBLIC_KEY": "-----BEGIN PUBLIC KEY-----\nxxxxxxxxxxxxxxxxxxxxx\n-----END PUBLIC KEY-----\n",
  "TENANT": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "DISCOVERY_DOCUMENT": "https://login.microsoftonline.com/<tenant>/v2.0/.well-known/openid-configuration",
  "SESSION_DURATION": 604800,
  "CALLBACK_PATH": "/_callback"
}
```

[nickshine/lambda-edge-azure-auth]:https://github.com/nickshine/lambda-edge-azure-auth
[local-exec]:https://www.terraform.io/docs/provisioners/local-exec.html
