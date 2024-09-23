# General information

In addition to the Single Sign-on, netID Partners can also use netID to enable users to manage their privacy settings. This offers a convenient, scalable and most importantly server-based/permanent way to manage a user’s privacy settings. To achieve this, netID supports the TCF 2.0 Standard of the IAB Europe.

netID (here specifically the netID Permission Center) offers the following services to integrate a netID Partner's Consent Management Platform. These APIs enable a Partner/his CMP to manage a TC String associated to an individual user. In addition, netID specific consents (netID Permissions) can be managed, which allow a netID Partner to identify a user while using his services.

In the following descriptions we will refer to the user’s overall privacy settings as **privacy status**.

!!! info  ""
    All permissions (TCF/netID specific) stored/managed using netID are always scoped to an individual netID Partner. That means in terms of the CMP, that netID only supports service-specific scoped TC Strings, and more importantly that the user’s explicit consent to be identified is managed/given per netID Partner.

## netID Permission Center

The netID Permission Center is a technical component in which consents and more generally the privacy status for netID user is stored and managed. For this purpose, the netID Permission Center offers various interfaces, which enable read and write access to this status.

### Services Overview

The following services are provided by the netID Permission Center to allow a CMP to store/manage a user’s privacy status for a specific netID Partner:

| service | meaning | endpoint (QA environment) | endpoint (LIVE environment) |
| ----------- | ----------- | ----------- | ----------- |
| READ SERVICE | Read the netID identifier (TPID), privacy status Sync-ID, netID Permissions and TC Strings for an individual user | einwilligungsspeicher.qa.netid.de | einwilligungsspeicher.netid.de |
| WRITE SERVICE | Write netID Permissions and TC Strings for an individual user | einwilligen.qa.netid.de | einwilligen.netid.de |
| DATA EXPORT SERVICE | Export the netID permissions and TC Strings for the respective netID Partner | einwilligungsuebersicht.qa.netid.de | einwilligungsuebersicht.netid.de |

### Custom privacy settings

Besides netID Permissions and TCF based privacy settings, digital services typically have bespoke/custom data processing purposes/scopes with respective custom settings. To enable netID users and partners to manage both the standardized settings as well as bespoke ones, netID Partners can choose to persist those custom settings outside the Permission Center in their own infrastructure. Partners may also choose to use the Sync-ID to maintain a full set of settings in their own infrastructure to allow for server-side synchronization of a users privacy status.

In order to store/manage these settings and assign them to returning users, partners can request access to a so called Sync-ID for an authenticated netID user. The Sync-ID is a subject identifier which is **different** for each client (`tapp_id`).  

It is only available in API responses if:

1. The user has chosen to use netID based privacy management with a specific partner in a prior interaction  - technically that means its only available in case the Permission Center does have an existing privacy status stored for that partner/user combination.
2. The partner explicitly requests the Sync-ID to be passed in reponses from the APIs. This is controller by setting a specific content/media type in the http accept header during the API calls.

!!! info  ""
    The Sync-ID is independent from the netID Identifier, its sole purpose is to enable the management of a custom privacy controls as described - specifically in cases where the user revokes / does not give the netID Permissions to a partner (thus the netID Identifier is not available to that partner), the overall privacy management (including custom controls) still functions independently.

## Read/Write Services

The READ and WRITE services are based on prior user authentication and are provided in two variants, with similar functions for the netID Partner's Consent Management Platform.

1. **Browser-based** API: Usage based on an already established user authentication stored within the respective browser (ex-ante)
2. **Token-based** API: Usage based on an access token requested via the netID Broker as described [here](access-token.md)

The distinction between browser- and token-based mainly relates to how an active user is authenticated before using the API/from where the APIs are being called.

!!! info  "Browser-based API usability"
    The browser-based API usage is based on a pre-existing authentication stored in a browser cookie (credentialed API call). In browser environments that block or partition third-party cookies by default the API will thus always return an error. netID Partners can rely on the token based [API](server-based.md) for integrations in these environments 

**Call information: parameters / header / cookies**

| name | type | function  | description |
| ----------- | ----------- | ----------- | ----------- |
| tapp_id | parameter | authentication | provided during setup, must be passed with each request. |
| origin | header | authentication | is passed by the browser for each XMLHttpsRequest (AJAX). The value must be a URL registered for this netID Partner (TAPP) |
| access | header | content type | determines the expected response/media type, two options are available to define an expected response with and without a Sync-ID to manage privacy controls |
| tpid_sec | cookie | user authentication | is located in the netid.de domain and is automatically passed on by the browser - if available (browser-based API) |
| token | parameter | access token | can be retrieved by the partner via the SSO process, is passed to access the API/to identify the user (token-based API) |

## Data export service

Using this API netID Partners can retrieve the privacy status with respect to netID Permissions and TC strings independent of users visiting their online properties. This allows for backend synchronization for netID Partners to clean-up / update their server-side storage - e.g. purging data in case of withdrawal of consent from an end-user.

## Authentication for API usage

Authentication of netID Partners for the browser-based APIs is handled via the parameter `tapp_id` and the `origin` header. Access is secured via [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).

- Multiple URLs are allowed per partner (`tapp_id`). These URLs must be registered in advance
- The read/write request must be made from an eligible URL

Authentication for the export API and token-based APIs is handled as follows.

- Token-based API: The user-specific read/write access is secured via access token (authentication).
- Export API: Basic authentication

## User authentication when using APIs

The authentication of the individual netID user depends on the API that is used, with `tpid_sec` (browser-based) or `token` (token-based).

`tpid_sec` is an encrypted ID token (JWT) which is stored on the domain netid.de as part of the login process via netID SSO/login by the netID Account Provider. This token is not accessible for netID Partners/the CMP.

The access `token` can be retrieved by a netID Partner during the login process via netID SSO in the form of a claim (OpenID Connect). This enables read/write access independently of the browser session (limited in time).

If, depending on the context, the `token` or the `tpid_sec` are not available, expired or invalid, a partner cannot access the Permission Center.
