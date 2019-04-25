# Exchange basic authentication

This sample show you how to use exchange remote basic authentication

```
"Exchange": {
    "Filter":"*",
    "UseRemote":true,
    "Credentials": {
        "login": "lsidev\\administrateur",
        "password": "@dm1n1str4t3ur"
    },
    "FQDN": "srvexchange2013"
}
```
To use basic remote authentication you have to set the property **UseRemote** to **true**, then you have to set **login** and **password** from an account that can access the Exchange Server.

*You have to keep in mind that Letsignit doesn't use these credentials. It's for exchange authentication only.*

Finally you have to set the **FQDN**, FQDN is the fully qualified domain name of your Exchange server.
For more information about the FQDN format, see the Microsoft documentation [here](https://docs.microsoft.com/en-us/powershell/exchange/exchange-server/connect-to-exchange-servers-using-remote-powershell?view=exchange-ps#connect-to-a-remote-exchange-server).