# Create Teams via Microsoft Graph


# What you need?
1. Register Power Automate as an Azure AD App and provide permissions to MS Graph 
2. Pre Defined Teams Templates
3. Microsoft Forms
4. Excel Online Workbook
5. Power Automate

## 1. Register Power Automate as an Azure AD App

For later activities you need to perform in Power Automate using MS Graph, you ned to make sure Power Automate is registered as an app by providing the consent.

You need **Global Admin** access to perform this action.

Go to Azure AD portal > App registrations > New Registration >
Provide the app name (eg: **Power_Automate_Graph_API**)
Supported Account Types: **Accounts in this organizational directory only**
Press **Register**

<img width="658" alt="image" src="https://user-images.githubusercontent.com/98259062/153370392-e32becc0-35d0-4375-8048-3d9abb47801a.png">

**Note down the Client ID of the APP**

<img width="796" alt="image" src="https://user-images.githubusercontent.com/98259062/153370593-57d2806e-4c71-46fb-90b8-bec6cf4baa3f.png">

### Secret
Go to **Certificates and Services** > **New Client Secret** > Set the name and expiration period
**note down the Secret (Value)**

<img width="950" alt="image" src="https://user-images.githubusercontent.com/98259062/153370243-70d100db-96f5-492f-a24d-76a74aaca6ad.png">


Now go to **API permissions**
Go to **Add a permission** > select **MS Graph** > select **Application permissions**

According to the official MS Documentaion, the below permissions requires for the applocation
Team.Create, Teamwork.Migrate.All, Group.ReadWrite.All**, Directory.ReadWrite.All**

Once the above permissions are added, provide **Admin consent**

This completes the app registration and providing MS Graph the necessary permissions.

<img width="746" alt="image" src="https://user-images.githubusercontent.com/98259062/153370747-cdc973a3-75f9-48a1-8de4-40b885e9b545.png">

## 2. Pre Defined Teams Templates

You can use the pre-defined templates in the Teams Admin Center
Teams Admin Center **>** Teams **>** Teams Templates

When you open the preffered Template, note down the Templete ID
eg: com.microsoft.teams.template.ManageAProject

If you create a new Template according to your requirement (custom template), then the Template ID would look something like this
eg: a8643242-c5e5-444d-813b-b191hc3adb71


## 3. Create a simple Form using Microsoft Forms

You need the below 'required' questions in the Form
1. Team Name
2. Team Owner
3. Template Name (drop down)

A bit about the Template Name.
This Template name must corralate with the previously noted templates. Ideally if you are planning on using 5 templates, you need to know the Template names and the IDs.

<img width="583" alt="image" src="https://user-images.githubusercontent.com/98259062/153369440-c9a93455-4997-4580-8099-b1963ce25746.png">


## 4. Excel Online Workbook
Create a simple Excel Online workbook and add a Table.
Name your Table and the columns
Eg: Table Name: Table1
Columns: TemplateName, TemplateID

Save the file in a OneDrive or in a Docuemnt Library

## 4.Power Automate
This is the most interesting part. To create the Power Automate flow by using the above elements.
Please check the **Solution** file for the Power Automate Flow.

## When all above steps are done, go to the file [Solution](https://github.com/shehanperera85/Teams-via-MS-Graph-and-Power-Automate/blob/main/Solution.md#how-to-create-the-power-automate-flow) 
