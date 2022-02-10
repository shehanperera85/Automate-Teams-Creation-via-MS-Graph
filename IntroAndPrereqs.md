# Create Teams via Microsoft Graph

Goal of this flow: To be able to automate the Teams creation by ingesting the preferred template.

Often times the issue with the IT Admins is with the ever growing Teams popularity, how to beat the demand and how to create Teams and specially, how to template it out and automate it.
Well, Teams templates are now in the Teams Admin Center where you can see pre-defined templates and the ability to cerate custom templates if required.
With the templates, IT admins have to potentially provide the users the ability create Teams and then advice them to create a Team with a template. This will also give them the opportunity to create more Teams without the knowledge of the IT.
Microsoft have introduced Teams templates sometime ago so the Admins can use the pre-defined ones or custom ones according to the user requirement. The idea is to bring uniformity across the board.
Template can bundle up Channels, Tabs and Apps

When Powershell fails, MS Graph comes to rescue! Why I say this is when you run the new-team command with the -template parameter, it will throw an error if you are not an Education customers (namely if you don't have EDU_Class" or "EDU_PLC licenses)
Of course you can use powershell to run MS Graph, but what I'm showcasing is a way to automate Teams creation via MS Graph using Power Automate.

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