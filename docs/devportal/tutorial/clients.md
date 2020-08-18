# Clients

Using clients you can manage the technical details for an integration into your services. **Services** may have multiple clients to cater for different types of integration (mobile, website, ...).

## Lifecycle

**Clients** have a simple lifecycle, once they are created they immediately get into the **active** state and can be used. At any point in time you can choose to

1. [Delete](#delete-a-client) a specific client, which puts it into the state **deleted**. Clients remain in the state deleted for 14 days, once these are passed it will be permanently removed. Within the 14 days grace period clients can be [re-activated](#reactivate-a-client) and return to into the **active** state.

2. [De-active](#deactivate-a-client) a specific client which puts into **inactive** status (disabling its usage). It can be [re-activated](#reactivate-a-client) and returns to into the **active** state.

!!! info ""
    Status changes on the overall [service](services.md) this client belongs to will also have immediate effect on all of its clients.

## Detailed Functionality

### Creating a Client

To create a client for a service, select **Add client** in the [details view](services.md#service-details-view) of the service. Client Details can be defined in the provided form.

![netid](../../images/devportal/netid_dev_portal_add_client.png){: style="width:50%;display: block; margin: 0 auto;" }

Fill out the necessary details, most importantly in case this client is meant for production use make sure that the **Callback URL** points to the same backend that operates this specific service. While this is not technically enforced, the callback URL must be operated by your company.

!!! info ""
    Please note that netID uses [pairwise subject identifiers](/sso/#general-overview), which are derived respective to the **clients callback url** (more specifically the **hostname** portion) set here. If you're using multiple clients for a service, you may want to use callback urls with identical host portion to avoid receiving different `sub` values for the same user.

Once the client is created you can retrieve the necessary credentials to integrate into your environment by expanding the client details, namely **Client ID** and **Client Secret**.

Depending on the status of the clients service w.r.t.[approval for production use](services.md#approval-for-production-use) the **Client Secret** will be shown as

* **Client secret - sandbox**: which indicates that the service is still in sandboxed mode
* **Client secret - live**: which indicates that the service has been approved to be used in a production environment

!!! warning "Client secret after service approval"
    Please note that the **Client Secret** does not change when the service is approved for production use, that means you do not need to change the configuration of your client / take action after the approval.

### Edit a Client

To edit a client select **Edit** in the **Clients** listing of the [details view](services.md#service-details-view) of the respective service for this client. Client details can be edited in the provided form.

Make the desired changes and updates and save the information by confirmation using **Update Client**.

### Deactivate a Client

To temporarily deactivate a client select **Edit** in the **Clients** listing of the [details view](services.md#service-details-view) of the respective service for this client.

In the client details form select the **Inactive** in the drop down menu under **Status**.

### Reactivate a Client

To reactivate a client select **Edit** in the **Clients** listing in the [details view](services.md#service-details-view) of the respective service for this client.

In the client details form select the **Active** in the drop down menu under **Status**.

### Delete a Client

To delete a client permanently expand the client details in the **Clients** listing of the [details view](services.md#service-details-view) of the respective service for this client.

Click on **Delete client** at the bottom of the expanded details and confirm the deletion. See notes on [lifecycle](#lifecycle)
