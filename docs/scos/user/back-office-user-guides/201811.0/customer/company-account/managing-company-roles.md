---
title: Managing Company Roles
description: Use the procedures to create, update, delete, and assign company roles in the Back Office.
originalLink: https://documentation.spryker.com/v1/docs/managing-company-roles
originalArticleId: d36afa06-1a49-4e55-a3b8-8677bfbeaeae
redirect_from:
  - /v1/docs/managing-company-roles
  - /v1/docs/en/managing-company-roles
---

This topic describes the procedures of creating and managing company roles. This is one of the steps in the Company Account setup.
***
You can create a role only if a company exists.
***
To start managing company roles, navigate to the **Company Account > Company Roles** section.
***

## Creating a Company Role
To create a new company role:

1. On the **Overview of Company Roles** page, click **Add Company User Role** in the top right corner.
2. On the **Create Company Role** page, enter the required information: select **Company** from the drop-down list and fill in the **Name** of the Company Role.
3. Selecting **Is Default** means that the role will be applied to all new company users automatically.
4. In the **Unassigned Permissions** section, select as many permissions as you need by selecting the checkboxes on the left of each value.
5. Once done, click **Save**.
***
## Editing a Company Role
To edit a company role:
1. On the **Overview of Company Roles** page in the _Actions_ column, click **Edit**  if you want to change the details for a company role.
2. On the **Edit Company Role** page, update the needed attributes.
***
## Deleting a Company Role

To delete a company role:
1. On the **Overview of Company Roles** page in the _Actions_ column, click **Delete**.
2. On the confirmation page, click **Delete** company role to confirm the action.
    {% info_block infoBox "If you delete a default role, the following message is displayed:" %}
_You cannot delete a default role; please set another default role before the delete action._
{% endinfo_block %}
***
**What's next?**
Once the role is created, you can proceed with creating a company user and assign the created role to it.
See [Managing Company Users](/docs/scos/user/back-office-user-guides/{{page.version}}/customer/company-account/managing-company-users.html) to know how the company users are created and managed.