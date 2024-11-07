---
title: 'Exchange - Creating contact groups'
excerpt: 'Find out how to manage mailing lists in Exchange'
updated: 2024-11-07
---

<style>
.w-600 {
  max-width:600px !important;
}
.h-600 {
  max-height:600px !important;
}
</style>

## Objective

Exchange groups enable multiple participants to communicate by sending emails to a unique group address. With this collaborative feature you can create and manage mailing lists that include Exchange users as well as external contacts.

**This guide explains how to use Exchange groups via the OVHcloud Control Panel and Outlook Web App (OWA).**

## Requirements

- access to the [OVHcloud Control Panel](/links/manager)
- an [OVHcloud Exchange solution](/links/web/emails-hosted-exchange) already set up

## Instructions

### Creating a new group

First, log in to your [OVHcloud Control Panel](/links/manager), navigate to the `Webcloud`{.action} section, and select your Exchange service from the column under `Microsoft`{.action} `Exchange`{.action}. Click on the `Groups`{.action} tab in the horizontal menu.

![contactgroups](images/exchange-groups-create01.png){.thumbnail .w-600 .h-600}

Clicking on `Create a contact group`{.action} will open a new window where you can define the group's settings:

![contactgroups](images/exchange-groups-create02.png){.thumbnail .w-600 .h-600}

- **Email address**: Set a new address to send messages to the mailing list. Please ensure that you are not using an address that is already working.
- **Group name**: Use the name that appears in your [OVHcloud Control Panel](/links/manager) and in your [OVHcloud web email](/links/web/email) (OWA).
- **Maximum ingress or egress size** : You can specify the maximum size of ingress and egress emails.
- **Hide in Outlook** : When this box is ticked, the group address will not appear in the list of Exchange service addresses.
- **Authentication required** : When this box is ticked, only users on the same platform will be able to send messages with the group address.

Click `Next`{.action} to continue.

On the second page, select the **Contacts** for the group and designate the **Administrators**. These choices will only be made from the email addresses and external contacts already listed in the service.

- **Administrators**: Email accounts authorized to send an email to all group contacts.
- **Contacts**: Email accounts that will receive emails sent to the group by administrators.

> [!primary]
>
> Please note that administrators must be configured as **Contacts** in order to receive group emails.

![contactgroups](images/exchange-groups-create03.png){.thumbnail .w-600 .h-600}

Click `Next`{.action} to continue and click `Confirm`{.action} to finalize your choices.

### Manage groups

After you create your group, you can change the settings that you set. To do this, click`...`{.action} to the right of the group in the table.

![contactgroups](images/exchange-groups-options01.png){.thumbnail .w-600 .h-600}

#### Manage users in a group

To add `Contacts` to your group or define `Administrators`, click the ``...`{.action} button, then `Configure users `{.action}. Tick the attributes that you want to attach to the email addresses in the `Email account` column.

> [!primary]
>
> A group can contain a maximum number of 10,000 contacts.

![contactgroups](images/exchange-group-options-users01.png){.thumbnail .w-600 .h-600}

#### Manage group delegations

The menu option `Configure delegations`{.action} will appear. This option allows you to delegate access in the same way as for an Exchange account. Find all the details in [this guide](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/feature_delegation).

![contactgroups](images/exchange-groups-options-delegation01.png){.thumbnail .w-600 .h-600}

> [!primary]
>
> Please note that any changes to this service may take a few minutes to be applied. You can check the status of most operations by selecting the `More`{.action} and `Recent tasks`{.action} options from the horizontal menu.

### Messaging a group in OWA

You can now test your mailing list via [OVHcloud webmail](/links/web/email) (OWA): simply send an email to the group address.

![contactgroups](images/exchange-groups-step6.png){.thumbnail}

## Go further

[Delegating permissions on an Exchange account](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/feature_delegation)

[Using the Outlook Web App with an Exchange account](/pages/web_cloud/email_and_collaborative_solutions/using_the_outlook_web_app_webmail/email_owa)

[Sharing calendars in OWA](/pages/web_cloud/email_and_collaborative_solutions/using_the_outlook_web_app_webmail/owa_calendar_sharing)

For specialised services (SEO, development, etc.), contact [OVHcloud partners](/links/partner).

If you would like assistance using and configuring your OVHcloud solutions, please refer to our [support offers](/links/support).

Join our [community of users](/links/community).