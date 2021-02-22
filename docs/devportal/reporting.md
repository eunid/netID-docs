# Reports

## Overview

The netID Developer Portal provides KPIs in individual reports as .cvs files for you to download. Here you can find an overview of the reports provided by the netID Developer Portal.

### General Information

- **Reporting interval**: daily
- **Aggregates**: Rolling time windows, aggregated to 1 day, 7 days, 30 days
- **Reporting period**: A report contains a maximum of 366 days
- Reports are calculated for the partner and each of his existing Relying Party. Each Relying Party will have its figures and the figures of its partner displayed as a sum.

### Reports in the netID Developer Portal

| Report|Description|Screen / process reference|
|---|---|---|
| Broker Screen ([Date]\_BrokerDialog\_*.csv)| The report shows how often the netID login flow was started, triggered by a click on the netID login button on the Relying Party page | netID UI Flow Step1: "Enter email address".|
| Broker "new netID User" Screen ([Date]\_BrokerNeuerNutzerDialog\_*.csv) | The report shows the number of entered e-mail addresses that are not yet netID-enabled. These addresses were entered in the Broker dialog by the netID user. | netID UI Flow Step1_redirect: "unknown user" page.|
| Broker Process ([Date]\_BrokerProcess\_*.csv)| The report shows the number of e-mail addresses entered in the first screen of the netID flow. A distinction is made between successful and unsuccessful attempts. The attempt is successful if the entered email address is known in the netID login context and unsuccessful if the email address is incorrect or could not be assigned. **Note:** Only events triggered via the broker screen are counted.| - |
| Broker master data transfer ([Date]\_BrokerStammdatenuebertragung\_*.csv) | The report provides information on the number of master data transmitted by the netID account provider to the Relying Party. It shows required and optional master data as a total. | - |
| Authentication Screen ([Date]\_AuthentifizierungDialog\_*.csv)| This report shows how many netID users wanted to sign-in with netID and successfully entered their e-mail address on the broker page. On this screen, the user is prompted to enter the password.| netID UI Flow Step2: Account Provider "enter password page"|
| Authentication Process ([Date]\_AuthentifizierungProzess\_*.csv)| The report provides information on how many netID users have completed the authentication process by entering a password. The report shows both successful and unsuccessful authentications. | - |
| Authorization Screen ([Date]\_AutorisierungsDialog\_*.csv)| The report informs how often the consent page was displayed. The page is displayed when the netID user logs in to the Relying Party for the first time, the Relying Party requires new/different master data of the netID user or the Relying Party explicitly requests the consent page.  **Note:** Unique users are also shown.| netID UI Flow Step3: Account Provider "Consent Page"|
| Authorization Process ([Date]\_AutorisierungsProzess\_*.csv)| The report shows how often mandatory and voluntary (as a total) or only voluntary master data were transferred after confirmation on the Consent page. **Note:** Unique users are also shown. | - |
| Authorization Process Core Data ([Date]\_AutorisierungProzessCoreData\_*.csv)| The report provides information on which master data (claim) was authorised via the consent page. For each master data item, the total number of approvals is reported. Mandatory and voluntary consents are shown as a total. **Note:** This report only contains **daily aggregates**. | - |
| Registration Neutral Instance Screen ([Date]\_RegistrierungNeutraleInstanzDialog\_*.csv) | The report shows how many netID account registration attempts were initiated by the user.| netID UI Flow Step1_b: Account Provider "registration page" for unknown users.|
| Registration Neutral Instance Process ([Date]\_RegistrierungNeutraleInstanzProzess\_*.csv)| The report shows the number of successful and unsuccessful registrations. | - |
| SSO active user ([Date]\_SSOAktiveUser\_*.csv)| The report provides information on the number of active users for the specified period, separated by partner and its Relying Party. A user activity is defined by a successful login. | - |
| SSO user ([Date]\_SSOUser\_*.csv)| The report provides information on the changes in the number of SSO users. | - |
| SSO user first use ([Date]\_SSOUserErstnutzung\_*.csv)| The report evaluates the number of first use of netID separately by partner (total) and its reeling party. | - |

## Download Reports

The netID Developer Portal provides individual reports as .cvs files for download.

- To download a report, click on Reports in the navigation on the left.
An overview of all available reports is displayed.

- Click on download to the right of the report you wish to download.

- A notification appears asking you whether you want to open or save the report.

- Select whether you want to open or save the report by clicking on Open or Save/Save As.

- The desired report is downloaded.
