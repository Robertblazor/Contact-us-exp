# Contact-us-exp
##It's working now, and I added some necessary code lines to the corresponding files.
##Here is a blogpost to state what I did.

####Is it possible to have an alternative to Twilio SendGrid, Mail gun, or other third-party communication Software as a Service that drives me nuts on verification and compliance?

####There is one offered by Microsoft built-in on Azure, and it can be easily integrated into Azure functions, as a backend function. Let's dive in.

####First, we need to select the service we need from Azure, like here:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mgl1a4us11piu8880rfm.png)

And under the page, look for this one icon with a name of Azure Email communication Service Domain.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bym9xnrh55voy01f536f.png)

###Second, just follow the configuration steps listed on this blogpost.

https://learn.microsoft.com/en-us/azure/communication-services/quickstarts/email/create-email-communication-resource

###Now, we can pick a starter template from GitHub and create a repo.
https://github.com/staticwebdev/blazor-starter

Note if you want to create your own repo from scratch, it's also okay. Here are some CLI commands you can reference:
`dotnet new blazorwasm -f net6.0 -n "Client"`
`dotnet new classlib -f net6.0 -n "Shared"`
'func init'
'func new'
'dotnet new sln -n "Repo-Name"'
'dotnet add reference ..\classlibName\classlibName.csproj'

If the following cli doesn't work, here is a different tutorial you can reference.

'func init'

Alternative GUI method in Visual Studio Code:

https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp

Now, got to your Api folder, type or copy the following commands:
'dotnet add package Azure.Communication.Email --version 1.0.0'
'dotnet add package Microsoft.ApplicationInsights.WorkerService --version 2.22.0-beta3'

Type the following command
'func new --template "HttpTrigger" --name "SendEmail"'

And reference to this repo as I did (Thanks to Mike) for the C# part of the function.

https://github.com/mikepfeiffer/azure-serverless-contact

This function won't run as you made the change, please, go ahead and edit the local.settings.json file, as I did:
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "AzureCommunicationServicesConnectionString": "<Your Connection String>",
    "myEmailAddress":"<Your Email to receive the email>",
    "senderEmailAddress":"<System assigned email address or your custom email address to host the service>"
  },
  "Host": {
    "LocalHttpPort": 7071,
    "CORS": "*"
    }
}
And the serviceDependencies.json to the following:
{
    "dependencies": {
      "storage1": {
        "type": "storage",
        "connectionId": "AzureWebJobsStorage"
      },
      "appInsights1": {
        "type": "appInsights",
        "connectionId": "<Azure communication service connection key>",
        "dynamicId": null
      }
    }
  }

You can test the function with the following CLI
'func start'

And you can also start your frontend.

Make two new files as Contact.razor and Contact.razor.css

Please use PostAsJsonAsync to invoke the Azure function API. and edit the page as you need to.

Here is my own Repo as open-source for everyone to use.

https://github.com/Robertblazor/Contact-us-exp

##Hope it can be helpful.
