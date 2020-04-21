# Clients

## Creating a Client

Create a Client for this service by clicking on Add client.

![netid](../../images/devportal/netid_dev_portal_add_client.png){: style="width:70%;display: block; margin: 0 auto;" }

Please enter the relevant data here and make sure that the "Callback URL", needs to point to your backend and the prefix part is the same as your domain name in the service.

If your service is not activated the client will initially run in a sandboxed mode, which means it can only be used with whitelisted netID-Accounts (email addresses).

In order to successfully run through the initial integration add a test user (email address) to the whitelist by selecting **Add Test-Account** in the service section. Up to 10 accounts can be whitelisted per sandboxed client. Once the service is released the test users will be no longer needed and removed from the service.

You will find the client Id and client secret in the client details.
After activation of the service, your client secret will change from **netID Token - Sandbox** to **client secret**.

## Edit a Client

- Under the appropriate service, select the client that you want to be changed.
- Click **Edit** next to the Client name.

A text box will appear asking you to confirm the operation with your password.

- Enter the password that you created during the registration in the netID Developer Portal and confirm your entry by clicking on **Confirm**.
   
You now have the possibility to change the entered information about the Client.

- Make the desired changes and updates and save the information with a click on **Update Client**.

## Deactivate a Client

You might have the need to take out a client from the environment. For that you do not need to delete the client right away. You have the option to deactivate a client. Within 14 days, you can [reactivate the client](#reactivate-a-client) before it gets finally deleted and removed from the overview.

- Under the appropriate service, select the client you want to be disabled.
- Click **Edit** next to the Client name.

A text box will appear asking you to confirm the operation with your password.

- Enter the password you created for logging into the netID Developer Portal and confirm your entry by clicking on **Confirm**.

You now have the possibility to change the status of the Client.

- To deactivate the client, select the entry Inactive in the drop down menu under Status.

## Reactivate a Client

A deactivated client remains in the overview. The status of the deleted client is set to DELETE. This gives you the opportunity to reactivate a deactivated client within 14 days before it is finally deleted and removed from the overview.

- Under the appropriate service, select the client to be reactivated.
- Click the arrow next to the Client name to expand the entire Client.
- Click **Reactivate Client** under the Client Status.
- To finally reactivate the client, confirm the process with your developer account password.

## Delete a Client

- Under the appropriate service, select the client to be removed.
- Click the arrow next to the Client name to expand the entire Client.
- Click **Delete Client** below.

A text box will appear asking you to confirm the operation with your password.

- Enter the password that you created during the registration in the netID Developer Portal and confirm your entry by clicking on **Confirm**.

!!! info ""
    You have the possibility to reactivate the client within 14 days before it is finally deleted and removed from the overview.
