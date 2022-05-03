# Requesting Access Tokens

In order to access the [server-based API](server-based.md) netID Partners can request an access token using the netID Broker in order to allow their Consent Management Platform to access the API on the users behalf.

To request an access token netID Partners request the scope `permission_management` when initiating an authentication flow via the netID Broker. This is supported both in conjunction with a Single Sign-on (meaning a full OpenID Connect flow with the transfer of a users personal data as requested) or standalone (meaning an OAuth 2.0 flow that only yields an access token).

## Requesting an access token with Single Sign-on

Which flow is executed is controlled via the `scope` parameter, requesting an access token in conjunction with a Single Sign-on flow is indicated by `scope=openid permission_management`

The below example starts a Single Sign-on flow requesting access to a users email as well as an access token.

```bash
https://broker.netid.de/authorize?
    response_type=code&
    client_id=[clientID]&
    redirect_uri=[redirect_uri]&
    scope=openid permission_management&
    claims={
        "userinfo":{
            "email":{"essential":true}
        }
    }
```

Details on the netID Broker APIs can be found [here](../../sso/), the access token will be provided within the users ID Token from the [token endpoint](../../sso/#token-endpoint) as an additional claim `permission_management`.

**Example ID Token response with included access token:**

```json
{
    "aud": "caab84a6-861....", // client_id of the netID Partner
    "sub": "0lme_TXmA_TQ....", // users pairwise subject identifier
    "permission_management": {
        "access_token": "eyJhbGciOiJkaXIiLC....",
        "token_type": "bearer",
        "expires_in": 500 },
    "auth_time": 1598277720,
    "iss": "https:\/\/broker.netid.de\/",
    "exp": 1598278622,
    "iat": 1598277722
}
```

## Requesting an access token without Single Sign-on

Requesting an access token without an actual user Sign-on (i.e. transfer of personal data) is initiated by only providing the scope `permission_management`. In this case the netID Broker executes a standard OAuth 2.0 Flow

```bash
https://broker.netid.de/authorize?
    response_type=code&
    client_id=[clientID]&
    redirect_uri=[redirect_uri]&
    scope=permission_management
```

As a result the [token endpoint](../sso/#token-endpoint) returns only an access token scoped for access to the netID Permission Center.

**Example Token response:**

```json
{
    "access_token": "eyJhbGciOiJkaXIiLCJl..",
    "scope": "permission_management",
    "token_type": "Bearer",
    "expires_in": 499
}
```
