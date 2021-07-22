# Netskope

1.	Click the Deploy to Azure button below.  
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fsreedharande%2FNetskope%2Fmaster%2FNetskope%2Fazuredeploy_Netskope_API_FunctionApp.json%3Ftoken%3DAFM6V37RIMZPYKUE3ZFBT33A7H5KA)

2.	Select the preferred Subscription, Resource Group and Location.  

	Enter the Workspace ID, Workspace Key, API Key, and URI.  
	Use the following schema for the uri value: https://<Tenant Name>.goskope.com Replace <Tenant Name> with your domain.  
3.	The default Time Interval is set to pull the last five (5) minutes of data. If the time interval needs to be modified, it is recommended to change the Function App Timer Trigger accordingly (in the function.json file, post deployment) to prevent overlapping data ingestion.  

4.	The default Log Types is set to pull all 6 available log types (alert, page, application, audit, infrastructure, network), remove any are not required.  
	Note: If using Azure Key Vault secrets for any of the values above, use the@Microsoft.KeyVault(SecretUri={Security Identifier})schema in place of the string values. Refer to Key Vault references documentation for further details.  

# Post Deployment Steps
The `TimerTrigger` makes it incredibly easy to have your functions executed on a schedule. This sample demonstrates a simple use case of calling your function based on your schedule provided while deploying. If you want to change
   the schedule 
   ```
   a.	Click on Function App "Configuration" under Settings 
   b.	Click on "Schedule" under "Application Settings"
   c.	Update your own schedule using cron expression.
   ```
   **Note: For a `TimerTrigger` to work, you provide a schedule in the form of a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression)(See the link for full details). A cron expression is a string with 6 separate expressions which represent a given schedule via patterns. The pattern we use to represent every 5 minutes is `0 */5 * * * *`. This, in plain text, means: "When seconds is equal to 0, minutes is divisible by 5, for any hour, day of the month, month, day of the week, or year".**