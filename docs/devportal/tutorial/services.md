# Services

## Create a Service 

To start, log in into the [netID Developer Portal](https://developer.netid.de/login). Create a **service** for which you want to leverage the netID Single Sign-on. Select **Services** in the menu, click **Add service** and fill in the required details in the following screen.

![netid](../../images/devportal/netid_dev_portal_add_service.png){: style="width:70%;display: block; margin: 0 auto;" }

**Service domain** is the domain of your customer facing website. Also, links to data privacy information (**URL privacy policy**) and terms of usage (**URL terms of usage**) should be supplied. As a best practice use separate services for development and production environments.

!!! info ""
    Note: for testing purposes, you can actually enter any domain and URL values into this form, as they are not technically relevant in order to get the netID integration in Auth0 running

!!! Warning ""
    The details provided here will be used within the netID User Interfaces (Single Sign-on, Privacy Center). If you are deploying into a production environment make sure that to provide accurate information. These values will also be inspected before a service is allowed to be used without sandboxed mode.

To save your service, click on **Add service**.

The next step to start the integration of netID for that service is to create a **client** for it. For details see [client tutorial][1].
[1]: clients.md

## Activate a Service

Once you've run throught the technical integration, you can request your service to be approved for usage in a production environment (without limitation to test users). To start the process open the detailed view of the service you want to activate and click on **Request service release**.

!!! info ""
    The service details will be reviewed by the **EnID** and approved for production usage (not limited to test users)

## Edit a Service

To alter an already existing service navigate to the service details view by selecting **Services** in the navigation on the left and by clicking on **Details** for that service in the listing.
Click **Edit** next to the name of the service in the detail view.  

!!! info ""
    In order to change details of a service you will be prompted to re-enter you password.

Make the desired changes and updates and save the information with a click on **Update Service**.

## Delete a Service

To remove an already existing service navigate to the service details view by selecting **Services** in the navigation on the left and clicking on **Details** for that service in the listing.

- Select **Show more details**.
- Click **Delete Service**.
  
To permanently delete the service, confirm the process by re-entering your password.

!!! info ""
    The service will remain listed for the next 14 days with a status **DELETED**. Within that timeframe you can recover a deleted service before it is permanently deleted and removed from your service overview. [Reactivate a service](#reactivate-a-service)  

## Reactivate a Service

If you delete a service, this service is no longer active. However, you have the option to reactivate a deleted service within 14 days before it is permanently deleted and removed from your service overview.

To re-active an already deleted service, navigate to the services details view by selecting **Services** in the navigation on the left and clicking on **Details** for that service in the listing.

- Click **Show more details**.
- Click **Reactivate Service**.

To confirm the reactivation, confirm the process by re-entering your password. Once done the service will appear with an **Active** status.
