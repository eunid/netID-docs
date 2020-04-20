# netID Services

## Create a Service 

To start, log in into the [netID Developer Portal](https://developer.netid.de/login). Create a **service** for which you want to leverage the netID single sign-on. Select **Services** in the menu, 
click **Add service** and fill in the required details in the following screen. 

![netid](../../images/devportal/netid_dev_portal_add_service.png){: style="width:50%;display: block; margin: 0 auto;" }

Next to the name, which should describe your service, is the **Service domain** an important value.
The service domain is the domain of your customer facing website. 
Also, links to data policies information and terms of use should be supplied.

The Service domain will also be the prefix for the Client Callback which you need to enter in the client section. 

As a best practice please use seperate services for development and live environments. This guarantees you that the reporting covers onöy data for the specific case.

!!! info ""
    Note: for testing purposes, you can actually enter any domain and URL values into this form, as they are not technically relevant in order to get the netID integration in Auth0 running
 
Uploading your logo will help your future customer identify your service during the login process.   

To save your service, click on **Add service**.

For each service you can now create clients.
Please refer to the **Client Tutorial**.

## Activate a Service

In order to use a service in your live environment, it must be approved by the netID foundation.

- Open the detailed view of the service you want to activate.

![netid](../../images/devportal/netid_dev_portal_request_service_release.png){: style="width:50%;display: block; margin: 0 auto;" }

- Click on **Request service release**.

!!! info ""
    The service will be released by the netID foundation. After successful release you can use the service live.

## Edit a Service

- To change the details of a service you have already added, click **Services** in the navigation on the left.
- Under All Services, select the service whose details you want to update and click Details.
- Click on **edit** next to the name of the service.
- A text box will appear asking you to confirm the operation with your password. 
- Enter the password you created for registration in the netID Developer Portal and confirm your entry by clicking on Confirm. 

You now have the possibility to edit the information about the service. 
Make the desired changes and updates and save the information with a click on **Update Service**.

## Delete a Service

- To remove a service, click on **Services** in the navigation on the left and select the corresponding service from the overview.
- Click **Show more details**.
- Click **Delete Service**.
- To permanently delete the service, confirm the process with your Developer Account password.

!!! info ""
    You have the possibility to reactivate the service within 14 days before it is permanently deleted and removed from the overview.

## Reactivate a Service

If you delete a service, this service is no longer active. However, you have the possibility to reactivate a deactivated or deleted service within 14 days before it is finally deleted and removed from the system.

- In the service overview, select the service that you want to reactivate.
- Click **Details** next to Service names.
- Click **Show more details**.
- Click **Reactivate Service**.
- To finally reactivate the service, confirm the process with your developer account password.

!!! info ""
    The service has been reactivated. The status is now displayed again as ACTIVE.