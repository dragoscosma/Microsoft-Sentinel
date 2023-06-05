# Get-AzureAD-CompanyName
Author: dragoscosma 👋

For any technical questions, please contact dcosma@microsoft.com  

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Enable-User%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Enable-User%2Fazuredeploy.json)

This playbook is intended to be automated from Microsoft Sentinel . It will get the CompanyName attribute for every user listed as an entity in the Sentinel Incident and post the value as a tag in the same Sentinel Incident.enable the Azure AD user accounts associated with the entities from Microsoft Sentinel incidents. 

#
### Recommendations:
<h5 align="left"><ul><li>Use a system assigned managed Identity. Location: Logic App - Identity - System assigned - Status: "On"</li></ul></h5>
<h5 align="left"><ul><li>Permissions: Assign Sentinel Responder role and Directory.Read.All to the system assigned identity</li></ul></h5>
<h6 align="left"><ul><i>Note: Sentinel Responder role will be an Azure RBAC permission and Directory.Read.All is an AAD permission.</ul></i></h6>


#
### Deployment

To configure and deploy this playbook:


Click the “**Deploy to Azure**” button and it will bring you to the custom deployment template.

In the **Project details** section:

* Select the **Subscription** and **Resource group** from the dropdown boxes you would like the playbook deployed to.  

In the **Instance details** section:  
                                                  
* **Playbook Name**: This can be left as "**AS-Azure-AD-Enable-User**" or you may change it. 

Towards the bottom, click on "**Review + create**". 

![Azure_AD_Enable_User_Deploy_1](Images/Azure_AD_Enable_User_Deploy_1.png)

Once the resources have validated, click on "**Create**".

![Azure_AD_Enable_User_Deploy_2](Images/Azure_AD_Enable_User_Deploy_2.png)

The resources should take around a minute to deploy. Once the deployment is complete, you can expand the "**Deployment details**" section to view them.
Click the one corresponding to the Logic App.

![Azure_AD_Enable_User_Deploy_3](Images/Azure_AD_Enable_User_Deploy_3.png)

Click on the "**Edit**" button. This will bring us into the Logic Apps Designer.

![Azure_AD_Enable_User_Deploy_4](Images/Azure_AD_Enable_User_Deploy_4.png)

Before the playbook can be run, the Azure AD connection will either need to be authorized in the indicated step, or an existing authorized connection may be alternatively selected. This connection can be found under the third step labeled "**For each**".

![Azure_AD_Enable_User_Deploy_5](Images/Azure_AD_Enable_User_Deploy_5.png)

Expand the "**Connections**" step and click the exclamation point icon next to the name matching the playbook.
                                                                                                
![Azure_AD_Enable_User_Deploy_6](Images/Azure_AD_Enable_User_Deploy_6.png)

When prompted, sign in to validate the connection.                                                                                                
![Azure_AD_Enable_User_Deploy_7](Images/Azure_AD_Enable_User_Deploy_7.png)

<br>
<br>
<p align="left">
<a href="https://linkedin.com/in/dragosco" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="dragosco" height="30" width="40" /></a>
</p>
