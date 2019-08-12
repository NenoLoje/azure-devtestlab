# Azure Lab Services Sample

This code sample demonstrates how you can build RDP files for all types of VMs in Azure Lab Services. Specifically, you will be able to retrieve VMs for the following conditions:
* As a professor, when the lab account is using the default virtual network configuration provided
* As a professor, when the lab account has virtual network peering enabled
* As a professor but for a single student, when the lab account is using using the default virtual network configuration provided

## How to set up your project
The sample will require you to authenticate against your lab account in order to retrieve the virtual machines in your lab. You will need to set up an application registration in order to use the code as provided. You can always change the CreateCredentials method in the Utilities class to choose a different method of authenticating.

1. [Create a lab account](https://docs.microsoft.com/en-us/azure/lab-services/classroom-labs/tutorial-setup-lab-account) if you do not already have one, and make sure there is a lab with some virtual machines in it.
1. [Create an App Registration](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#create-an-azure-active-directory-application) in AAD.
1. [Grant your App Service a role](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#assign-the-application-to-a-role) on the subscription your lab account is in (you can give more granular permission as appropriate to the scenario you are testing).
1. Update the App.config in the sample project with the ClientId, secret, tenant, and subscription for your app registration.
1. Update the App.config in the sample project with the folder you want to save th RDP files to, as well as the lab account name, lab name, and resource group name. The folder must already exist on disk.
1. If you are interested in testing the third scenario, you will need to also set the username of the student in the App.config.

Now you should be able to run the solution and create the RDP files.

## Project parameters

You will need to provide one of three parameters when you run the project:
* getPublicRdpFilesForLab: This is for the typical scenario of an app with professor permissions trying to retrieve all the RDP files for all the student virtual machines.
* getPrivateRdpFilesForLab: This is the same as above, but this is for lab accounts with vnet peering enabled.
* getPublicRdpFilesForUser: This is for the scenario of an app with professor permissions trying to retrieve all the RDP files for a single student, across labs.