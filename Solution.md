# How to Create the Power Automate Flow

In this section, I'm discussing the flow. Once it's all done, you will be able to automate the Team creation by ingesting the preferred template.

## Step 1 - Create the trigger
This should be **When a new responce is submitted** and select the previously created MS Form [Check here](https://github.com/shehanperera85/PowerAutomate/blob/main/IntroAndPrereqs.md#3-create-a-simple-form-using-microsoft-forms
)

<img width="687" alt="image" src="https://user-images.githubusercontent.com/98259062/153371830-b05ab360-3de6-4cf5-b322-718a7a57fca8.png">

## Step 2 - (Action) Get Response Details
<img width="687" alt="image" src="https://user-images.githubusercontent.com/98259062/153371198-97cb373d-6036-4b3f-9367-1deb335ea6ea.png">

## Step 3 - (Action) Search for the user
This correlates with the Qurstion 4 of the form (Team Owner's First and Last Name or Email (please enter the correct details)
The reason is the form is unable to provide user @ mentoins or resolves usernames/ UPNs.
With the **Search for users (V2)** action in place, when you provide a part of the name (given nameor surname) email address, UPN it will search for the user from Azure AD

<img width="683" alt="image" src="https://user-images.githubusercontent.com/98259062/153372847-a9c2d59d-a38a-4317-9f38-cc18c788e867.png">

As you can see in the screenshot, it Search Term should be **Team Owner's name** from the Form.

## Step 4 - (Action) Get a row
This part correlates with the drop-down question 3 in the form **Template Nname**
<img width="682" alt="image" src="https://user-images.githubusercontent.com/98259062/153373414-9fdb3cc3-d470-4bba-872e-1c65b95909e7.png">

As per the steps mentioned in [Excel Online Workbook](https://github.com/shehanperera85/IntroAndPrereqs/blob/main/CreateTeamsViaMSGraph.md#4-excel-online-workbook) you now have the workbook with the required template IDs in it.
Provide the necessary feileds as mentiond above.

## Step 5 - (Action) Use HTTP to invoke REST API

As you can see in the below screenshot, for **Select an Output from the previous steps** and select **Value** from the **Dynamic Content** box.
<img width="687" alt="image" src="https://user-images.githubusercontent.com/98259062/153374061-c37a5bb4-45eb-479f-b4e2-cafa34bb5c31.png">

In the HTTP REST API function, the below information should be filled.

**Method**  : POST

**URI**     : https://graph.microsoft.com/beta/teams

**Headers** : Content-type    application/json

**Authentication**  : Active Directory OAuth

**Tenant**          : _Azure AD Tenant ID_

**Audiance**        : https://graph.microsoft.com

**Client ID**       : Client ID from [App Registration step](https://github.com/shehanperera85/IntroAndPrereqs/blob/main/CreateTeamsViaMSGraph.md#1-register-power-automate-as-an-azure-ad-app)

**Credential Type** : Secret

**Secret**          : Secret Value from [App reg step](https://github.com/shehanperera85/PowerAutomate/edit/main/IntroAndPrereqs.md#secret)

**Body**            :
In the below code you can see **[ID]**, **[TEAM NAME] **and **[USER ID]**. They are the Dynamic Content I picked from the box acordingly. (See screenshot)

<img width="343" alt="image" src="https://user-images.githubusercontent.com/98259062/153375702-4249d8a4-bb5c-4b06-aeaa-2e6df666f15a.png">

{
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('[ID]')",
  "displayName": "'[TEAM NAME]'",
  "description": "The team for those in architecture design",
  "members": [
    {
      "@odata.type": "#microsoft.graph.aadUserConversationMember",
      "roles": [
        "owner"
      ],
      "user@odata.bind": "https://graph.microsoft.com/beta/users('[USER ID]')"
    }
  ]
}

