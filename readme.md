# PowerShell Script for Exchange Signature

Deploy-Signatures.ps1 is a PowerShell script for deploying Letsignit signatures in Exchange OWA.

You have to install at least Powershell version 4.
See [here](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-windows-powershell?view=powershell-6)

## Getting Started

Before using the script, you must identify yourself, you can do this by getting your AppId and generating at least one Secret on the Letsignit webapp. Then, add both to the Configuration file, just like shown below: 

```
{
    "appId": "c9b2691877ac4a3ba5997111b0e3248d",
    "appSecret": "&*#7G]SekXoqX427UQ7}X[#7Bz13Kv<5"
}
```

### Configuration File

You can customize your script using a configuration file. The file is in JSON. You have to save the file in the same place that you save the script.

#### appId & appSecret
For Authentication with Letsignit API we are using an appId and an appSecret.

#### Exchange
For the Exchange configuration:
```
"Exchange": {
        "Filter":"EmailAddresses -like '*virtual*'",
        "UseRemote":true,
        "Credentials": {
            "login": "virtualdevmib\\administrateur",
            "password": "administrateur",
            "securePassword":""
        },
        "FQDN": "srvexchange2016"
    }
```

#### Filter
The filter is the [Get-Mailbox](https://docs.microsoft.com/en-us/powershell/module/exchange/mailboxes/get-mailbox?view=exchange-ps) filter parameter for Exchange. Here, you can specify the mailboxes you want to get with the script. If you want to select all mailboxes you can set * as the value.
If you want to create a filter you have to make a filter on Mailbox properties using [Comparison Operators](https://docs.microsoft.com/fr-FR/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-4.0)
```
"Filter":"*"
```

#### UseRemote
If you put the script on the Exchange Server you should set **UseRemote** to **false**, otherwise if you use a local computer you should set it to true and use the authentication information below:

#### Credentials
The credentials are used to connect to the Exchange Server when **UseRemote** is defined to **true**. 
You have to set a login and a password from an account that can access the Exchange Server. You can choose between setting a password or a securePassword.

If you want to use a securePassword you have to convert your password to a secure string. Execute the comand below replacing *P@$$w0rd* with your password and put the result on the configuration file.
```
"P@$$w0rd" | ConvertTo-SecureString -AsPlainText -Force | ConvertFrom-SecureString
```
You have to keep in mind that Letsignit doesn't use these credentials.

#### FQDN
The FQDN property is also used to connect to the Exchange Server when **UseRemote** is **true**. 
FQDN is the fully qualified domain name of your Exchange server.
For more information about the FQDN format, see the Microsoft documentation [here](https://docs.microsoft.com/en-us/powershell/exchange/exchange-server/connect-to-exchange-servers-using-remote-powershell?view=exchange-ps#connect-to-a-remote-exchange-server).
#### ActiveDirectory
The active directory configuration is used to filter the mailboxes found with the Exchange configuration. If you want to use this part on a Windows 10, RSAT is required. For more information see [here](https://docs.microsoft.com/en-us/windows-server/remote/remote-server-administration-tools)

```
"ActiveDirectory": {
    "Filter":"mail -like '*letsignit*'",
    "SearchBase":""
}
```

#### Filter
The filter is the [Get-ADUSer](https://docs.microsoft.com/en-us/powershell/module/addsadministration/get-aduser) Filter parameter. Here, you can specify the users you want to get with the script.
If you want to select all users, you can set * as the value.
If you want to create a filter you have to make a filter on ADUser properties using [Comparison Operators](https://docs.microsoft.com/fr-FR/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-4.0)

```
"Filter":"*"
```

#### SearchBase
The SearchBase is the [Get-ADUSer](https://docs.microsoft.com/en-us/powershell/module/addsadministration/get-aduser) SearchBase parameter. Here, you specify an Active Directory 'Distinguished Name' to search under. If you don't specify a SearchBase, the script will get the current Domain DN.
```
"SearchBase":"CN=Users,DC=virtualdevlsi,DC=devlsi"
```

At this moment you can deploy the script and run it to configure Lesignit signatures to all the users you want to.

## Deployment
Download the script and put it on a Server that can access to your Exchange Server or it can be the Exchange Server itself. 
Then, fill out the script with your authentication parameters and specify the filters you want to use.
You can run the script each time you want to update your users' signatures, you can also create a scheduled task.

If you want to know more about running a Powershell script from the task scheduler see [here](https://community.spiceworks.com/how_to/17736-run-powershell-scripts-from-task-scheduler)
