# Get-AzureAD-CompanyName
Author: dragoscosma 👋     <a href="https://linkedin.com/in/dragosco" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="dragosco" height="25" width="30" /></a>

For any technical questions, please contact dcosma@microsoft.com  


[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdragoscosma%2FMicrosoft-Sentinel%2Fmaster%2FPlaybooks%2FGetAADUserCompanyName%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdragoscosma%2FMicrosoft-Sentinel%2Fmaster%2FPlaybooks%2FGetAADUserCompanyName%2Fazuredeploy.json)

This playbook is intended to be automated from Microsoft Sentinel. It will get the CompanyName attribute for every user listed as an entity in the Sentinel Incident and post the value as a tag in the same Sentinel Incident.enable the Azure AD user accounts associated with the entities from Microsoft Sentinel incidents. 

#
### Recommendations:
<h5 align="left"><ul><li>Use a system assigned managed Identity. Location: Logic App - Identity - System assigned - Status: "On"</li></ul></h5>
<h5 align="left"><ul><li>Permissions: Assign Sentinel Responder role and Directory.Read.All to the system assigned identity</li></ul></h5>
<h6 align="left"><ul><i>Note: Sentinel Responder role will be an Azure RBAC permission and Directory.Read.All is an AAD permission.</ul></i></h6>


#
### Deployment

Click the “**Deploy to Azure**” button and it will bring you to the custom deployment template.

In the **Project details** section:

* Select the **Subscription** and **Resource group** from the dropdown boxes you would like the playbook deployed to.  

In the **Instance details** section:  
                                                  
* **Playbook Name**: This can be left as "**GetCompanyNameFromAAD**" or you may change it. 

Towards the bottom, click on "**Review + create**". 

![Azure_AD_Enable_User_Deploy_1](Images/Get_AAD_CompanyName-create1.png)

Once the resources have validated, click on "**Create**".

The resources should take around a minute to deploy. Once the deployment is complete, you can expand the "**Deployment details**" section to view them.
Click the one corresponding to the Logic App.

![Azure_AD_Enable_User_Deploy_3](Images/Get_AAD_CompanyName-create2.png)

Click on the "**Edit**" button. This will bring us into the Logic Apps Designer.

![Azure_AD_Enable_User_Deploy_4](Images/Get_AAD_CompanyName-create3.png)

Before the playbook can be run, the Azure AD and Sentinel connection will either need to be authorized in the indicated step, or an existing authorized connection may be alternatively selected. 

Create a system assigned managed Identity. Under the Logic App click on: "Identity" - "System assigned", "On". Copy the Object ID.

![Azure_AD_Enable_User_Deploy_5](Images/Get_AAD_CompanyName-create_identity1.png)

In Azure assign this Identity the needed Azure role: Microsoft Sentinel Responder.
Azure - Subscription - IAM - Add - Add role assignment - choose: "Microsoft Sentinel Responder" - next - under members select: Managed Identity and then choose: "select members".
Here, choose under managed identity: "Logic app" and then select the newly created app.
![Azure_AD_Enable_User_Deploy_5](Images/Get_AAD_CompanyName-assign_perm1.png)

For the Azure AD permissions, you need to use PowerShell.
Commands:
Connect-AzureAD

$graph = Get-AzureADServicePrincipal -Filter "AppId eq '00000003-0000-0000-c000-000000000000'"
$Permission = $graph.AppRoles `
    | where Value -Like "Directory.Read.All" `
    | Select-Object -First 1

$msi = Get-AzureADServicePrincipal -ObjectId b61cc88f-2349-4574-a704-b597161c52b0

New-AzureADServiceAppRoleAssignment `
    -Id $Permission.Id `
    -ObjectId $msi.ObjectId `
    -PrincipalId $msi.ObjectId `
    -ResourceId $graph.ObjectId
![Azure_AD_Enable_User_Deploy_6](Images/Get_AAD_CompanyName-assign_perm2.png)

<br>
<br>
<p align="left">
<a href="https://linkedin.com/in/dragosco" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="dragosco" height="30" width="40" /></a>
</p>
