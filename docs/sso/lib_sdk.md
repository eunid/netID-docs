# Libraries and SDKs

## Use of SDKs

There are a large number of OpenID Connect client libraries available in many different language / deployment environments. Below, several examples will be given, along with tips for using them.

Many client libraries are listed at <https://openid.net/developers/libraries/>

## Native Apps

Native mobile apps or single page applications that authenticate the user within the app via authorization code flow can leverage the OpenID Foundation AppAuth libraries with netID.  Both can be used with netID [clients](../../devportal/tutorial/clients/#creating-a-client) using custom schemes or claimed HTTPs URLs.

In addition netID also provides a dedicated SDK that allows for more convenient user flows as well as a convenience wrapper for the token-based [CMP integration](../../cmp/server-based/).

### App2App netID SDKs

In order to streamline the integration both for Single Sign-on as well as the token based [CMP integration](../../cmp/server-based/) into native mobile apps, netID is providing a standardized SDK both for iOS and Android. The SDK is provided as an open source component and is based on the AppAuth libraries for the respective platform. 

netID users who already have a mobile app of their netID account provider installed on their mobile device, especially the email apps of GMX and WEB.de, can log into the apps of netID partners using these apps by using the netID SDK. This dramatically simplifies the login process - 1 click to login, 2 clicks to register for the first time in the app of a netID partner. 

Details can be found directly on GitHub 

* [netID SDK for Android](https://github.com/eunid/netid-sdk-android)
* [netID SDK for iOS](https://github.com/eunid/netid-sdk-ios)

### Android

[AppAuth for Android](https://github.com/openid/AppAuth-Android#readme) must be used with [Client Types](index.md#client-types) **'Native / Mobile App (PKCE)'**. AppAuth for Android supports requesting user claims both via scopes and the claims parameter - cf. to [Claims and Scopes](index.md#claims-and-scopes)

### iOS

[AppAuth for iOS](https://github.com/openid/AppAuth-iOS#readme) must also be used with [Client Types](index.md#client-types) **'Native / Mobile App (PKCE)'**. AppAuth for iOS supports requesting user claims via scopes only as of now.

## Web-based

### General

Regardless of the choice of environment, it's possible to do the following preliminary experiments:

1. In the developer portal for the partner, create a service, request approval for it, and then create a client for it
2. When choosing which URLs to use, it's possible to generate locally applicable test environments by making an entry in the hosts file of a developer workstation at the endpoints given for service and client and creating and using self-signed certificates.
   > **Example** "Entry in hosts" <br>
   127.0.0.1  www.democlient.de <br><br>
   > **Example** "Creating a self-signed certificate" <br>
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem

3. Here, for the Common Name give the host name of the environment you want; so, in this case: www.democlient.de.
Using the Client Credentials from the developer portal, the local host entry, and the certificate with the key, it's possible to run through the netID requests.
4. When testing with browsers, it's a good idea to use private windows; otherwise cookies left behind from previous run-throughs may cause confusion.

### PHP

In PHP it's possible to use the package <https://github.com/jumbojett/OpenID-Connect-PHP>.

According to the instructions, the installation works out of the box. The package derives the *redirect_uri* from its own URL; here, the position of the script in the path of the web server can either be used as *redirect_uri* when creating the client or configured accordingly in the web server using rewrite rules.

!!! Info "Please ensure that Token Signing is enabled"
    Otherwise this library will not work without additional patches.

A simple sample client may then look like this:

```php
<?php

/**
 *
 * Copyright MITRE 2012
 *
 * OpenIDConnectClient for PHP5
 * Author: Michael Jett <mjett@mitre.org>
 *
 * Licensed under the Apache License, Version 2.0 (the "License"); you may
 * not use this file except in compliance with the License. You may obtain
 * a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
 * WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
 * License for the specific language governing permissions and limitations
 * under the License.
 *
 */

require __DIR__ . '/vendor/autoload.php';

use Jumbojett\OpenIDConnectClient;

// specify ClientID und secret!
$oidc = new OpenIDConnectClient(
    'https://broker.netid.de/',
    'example-clientid',
    'example-secret'
);

// if the default redirect_uri is not to be used, a custom value can be set here:
// $oidc->setRedirectURL('https://clientexample.org/callback');

// then however a URL-rewrite is necessary, as for example with mod_rewrite from apache:
// RewriteEngine On
// RewriteRule "^callback(.*)" "/client_example.php$1"

$oidc->authenticate();
$sub = $oidc->getVerifiedClaims('sub');

?>

<html>
<head>
    <title>Example OpenID Connect Client Use</title>
    <style>
        body {
            font-family: 'Lucida Grande', Verdana, Arial, sans-serif;
        }
    </style>
</head>
<body>

    <div>
        netID login successful, the Subject Identifier is: <?php echo $sub; ?>
    </div>

</body>
</html>
```

### Javascript

One highly recommended JavaScript implementation (node.js) of an OpenID Connect relying party can be found here: <https://www.npmjs.com/package/openid-client>

### Java

Spring Security examples for Java:

- GitHub:mitreid-connect/simple-web-app
- GitHub:eugenp/tutorials/tree/master/spring-security-openid

### Rust

A good OpenID Connect relying party client for Rust can be found here: <https://docs.rs/crate/oidc/0.2.0>.

### Go

For go the package GitHub:coreos/go-oidc makes a netID login possible. The package may be installed here:

```go
go get github.com/coreos/go-oidc
```

There is no explicit support for entering claims, essential or otherwise.

The simple example client netid.go first needs to be edited before Client Credentials, host name, and certificates may be entered, after which it can be run using:

```go
go run netid.go
```
