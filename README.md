# Azure Media Service Speech to Text Indexer Azure Function Pipeline

## Solution Overview

In summary, an audio asset is added to Azure Blob Storage, a Blob Storage trigger Azure Function copies the audio file to Azure Media Services Blob Storage and initiates a Media Analytics Indexer Job. On completion of the job an Webhook function is called and the job metadata is queued for consumption by the next process in the pipeline.

![Solution Overview](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speech-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/Media%20Indexer.jpg)


# Getting Started Resources

1. [Indexing Media Files with Azure Media Indexer](https://docs.microsoft.com/en-us/azure/media-services/media-services-index-content)
2. [Media Analytics on the Media Services platform](https://docs.microsoft.com/en-us/azure/media-services/media-services-analytics-overview)
3. [Use Azure AD authentication to access Azure Media Services API with .NET](https://docs.microsoft.com/en-us/azure/media-services/media-services-dotnet-get-started-with-aad)
4. [Develop Azure Functions with Media Services](https://docs.microsoft.com/en-us/azure/media-services/media-services-dotnet-how-to-use-azure-functions)


# Application Settings

## Create an Azure Active Directory Service Principal

When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:

1. User authentication authenticates a person who is using the app to interact with Azure Media Services resources. The interactive application should first prompt the user for credentials. An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming. 
2. Service principal authentication authenticates a service. Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.


**For Azure Media Services integrated with Azure Functions you need to create a service principal**


Azure Portal -> Azure Active Directory -> App registrations

### STEP 1: Add New application registration

![Active Directory Create Service Principal](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speach-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/ActiveDirectoryCreateServicePrincple.JPG)

### STEP 2: Select the newly created Service Principal

![List Service Principals](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speach-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/ActiveDirectoryListIdentities.JPG)

### STEP 3: Record Application ID.

This is the UUID (GUID) for the Service Principal you've just created. You will need this id when configuring the Azure Function 'IndexerBegin' app. 

![Service Principal](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speach-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/ActiveDirectoryServiceprincipalJPG.JPG)

## STEP 4: Create Service Principal Key

1. From All Settings, select Keys.
2. Create a new key, select duration.
3. Record Key, this is required for Azure Functions and is only visible when created.

![settings](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speach-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/ActiveDirectoryServiceprincipalKey.JPG)




## Keys

### AMSNotificationWebHookKey

![AMSNotificationWebHookKey](https://raw.githubusercontent.com/gloveboxes/Azure-Media-Service-Speach-to-Text-Indexer-Azure-Function-Pipeline/master/Resources/WebHookKey.JPG)

