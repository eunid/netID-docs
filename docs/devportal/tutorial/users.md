# User Management

The netID Developer Portal supports different roles with different levels of access, namely Developer and Representative. Creating a new developer portal account from scratch (and thus a new managed company profile) will assign you the role Representative. Roles can be [changed](#changing-the-role-of-a-user) and users can be [invited](#invite-a-new-user) to participate in the management of a company profile. For details on roles see [roles/rights](#rolesrights).

## Detailed Functionality

In order to access the user management functionality, navigate to **User Management** view by clicking on it in the left hand menu. This view lists all the active users and exposes the below described functionality.

![netid](../../images/devportal/netid_dev_portal_user_management.png){: style="width:70%;display: block; margin: 0 auto;" }

### Change personal data

Click on **Details** for the respective user in the User Management View.

![netid](../../images/devportal/netid_dev_portal_user_details.png){: style="width:70%;display: block; margin: 0 auto;" }

Make the desired changes and then confirm your entries by clicking on **Apply changes**.

### Invite a new user

To add relevant team members to your company profile, users with the role representative can invite new users. Click on **Invite User** in the User Management view.

Add the necessary details for the new user (name, email address, ...) and the role he will be assigned to once added. Choose the role carefully, see [roles/rights](#rolesrights) for details. To start the invitation process click on **Send invitation**, the invited user will receive an email with the necessary details.

### Changing the role of a user

Representatives can change the role of users at any point in time, by clicking **Details** for the respective user in the User Management View. Simply select a new role in the details dialog and confirm with **Accept changes**.

Choose the role carefully: Representatives have full administrative access, Developers can only manage the necessary technical details for clients, see [roles/rights](#rolesrights) for details.

!!! info ""
    At least one user must have the role Representative. Conflicting changes will be rejected.

### Delete user

Representatives can remove users at any point in time, by clicking **Details** for the respective user in the User Management View and clicking **Delete user account**.

!!! info ""
    At least one user must have the role Representative. Conflicting changes will be rejected.

## Company Profile Main Contact

To manage/adjust you general main company contact select **Company Profile** in the navigation on the left.

![netid](../../images/devportal/netid_dev_portal_company_details.png){: style="width:70%;display: block; margin: 0 auto;" }

Adjust the details under Contact details and click on **Apply Changes**.

## Roles/Rights

The following table show the rights per role:

|Function|Representative|Developer|
|---|:---:|:---:|
| View Service         |        X       |     X     |
| Create Service       |        X       |           |
| Edit Service         |        X       |           |
| Delete Service       |        X       |           |
| View Client          |        X       |     X     |
| Create Client        |        X       |           |
| Edit Client          |        X       |     X     |
| Delete Client        |        X       |           |
| Manage Test Users    |        X       |     X     |
| View Users           |        X       |Himself only|
| Invite Users         |        X       |           |
| Edit Users           | Own details + all roles|own details|
| Delete Users         |        X       |           |
| View Company Profile |        X       |     X     |
| Edit Company Profile |        X       |           |
