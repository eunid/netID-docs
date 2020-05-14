# General information

In addition to the Single Sign-on, netID Partners can also use netID to enable users to manage their general data protection settings regarding the data usage that they want to allow. This offers a convenient, scalable and most importantly server-based/permanent way to manage a user’s consent status or more generally a status in terms of legal grounds for commercial data usage. To achieve this, netID supports the TCF Standard of the IAB. 

netID (here specifically the netID Permission Center) offers the following services to integrate a netID Partner's Consent Management Platform. These APIs enable a Partner/his CMP to manage a TC String associated to an individual user. In addition, netID specific consents (netID Permissions) are made possible, with which a netID Partner is able to identify a user while using his services.

In the following descriptions we will refer to the user’s overall privacy settings as **privacy status**.

!!! info  ""
    All permissions (TCF/netID specific) stored/managed using netID are always scoped to an individual netID Partner. That means in terms of the CMP, that netID just supports service-specific scoped TC Strings, and more importantly that the user’s explicit consent to be identified is managed/given per netID Partner. netID doesn't support global scoped TC Strings.   

## netID Permission Center

The netID Permission Center is a technical component in which consents of netID users are stored. For this purpose, the netID Permission Center offers various interfaces, which enable read and write access.


## netID Permission Center Services

The following services are provided by the netID Permission Center to allow a CMP to store/manage a user’s privacy status for a specific netID Partner:

| service | meaning | server name (QA environment) | server name (LIVE environment)  | 
| ----------- | ----------- | ----------- | ----------- |
| READ SERVICE | Read the netID identifier (TPID), netID Permissions and TC Strings for an individual user | einwilligungsspeicher.qa.netid.de | einwilligungsspeicher.netid.de |
| WRITE SERVICE | Write netID Permissions and TC Strings for an individual user | einwilligungsspeicher.qa.netid.de | einwilligungsspeicher.netid.de |
| DATA EXPORT SERVICE | Export the netID permissions and TC Strings for the respective netID Partner | einwilligungsuebersicht.qa.netid.de | einwilligungsuebersicht.netid.de |

## Read/Write Services

The READ and WRITE services are based on previous user authentication and are provided in two variants, with similar functions for the netID Partner's Consent Management Platform.

1. **Browser-based** API: Usage based on an already established user authentication stored within the respective browser (ex-ante)
2. **Server-based** API: Usage based on an authentication token acquired via a Single Sign-on

The distinction between browser- and server-based mainly relates to how an active user is authenticated before using the API/from where the APIs are being called.

**Call information: parameters / header / cookies**

| name | type | function  | description |
| ----------- | ----------- | ----------- | ----------- |
| tapp_id | parameter | authentication | is provided by netID for each publisher upon activation and must be passed unchanged with each request. |
| origin | header | authentication | is passed by the browser for each XMLHttpsRequest (AJAX). The value must be a URL registered for this netID Partner (TAPP). |
| tpid_sec | cookie | user authentication | is located in the netid.de domain and is automatically passed on by the browser - if available (browser-based API). |
| token | parameter | user authentication/access token | can be retrieved by the partner via the SSO process, is passed to access the API/to identify the user (server-based API) |

## Data export service

The export API allows a partner to export the netID Permissions/TC String as well as deltas on those. The API is just available **server based**.

## Authentication for API usage

Authentication of netID Partners for the browser-based APIs is handled via the
parameter `tapp_id` and the `origin` header. Access is secured via
[CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).

- Multiple URLs are allowed per publisher (TAPP). These URLs must be registered in advance
- The read/write request must be made from an eligible URL

Authentication for the server-based APIs is handled as follows.

- The user-specific read/write access is secured via access token (authentication).
- Data Export uses basic authentication

## User authentication when using APIs

The authentication of the individual netID user depends on the
API that is used, with `tpid_sec` (browser-based) or `token` (server-based).

`tpid_sec` is an ecrypted ID Token (JWT) which is stored on the domain netid.de as part of the login process via netID SSO/login with the
netID Account Provider. This token is not accessible for netID Partners/the CMP.

The access `token` can be retrieved by a netID Partner during the login process via netID SSO in the form of a claim (OpenID Connect). This enables read/write access independently of the browser session (limited in time).

If, depending on the context, the `token` or the `tpid_sec` are not available, expired or invalid, a publisher cannot read/write the TC
String and of course cannot access the TPID.