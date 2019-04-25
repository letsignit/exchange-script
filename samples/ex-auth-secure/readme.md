# Exchange secure authentication

This sample show you how to use exchange remote secure authentication

```
"Exchange": {
    "Filter":"*",
    "UseRemote":true,
    "Credentials": {
        "login": "lsidev\\administrateur",
        "securePassword": "01000000d08c9ddf0115d1118c7a00c04fc297eb010000001163fe27ecd6294a92c3979e719f722a0000000002000000000003660000c00000001000000099c443befa4a3480dc92861e79581bdf0000000004800000a00000001000000038b5aba5ed0b33d86cae9d85b7e07594200000006d6335ee82797996c6089745dbd723e80d5aac58cebbf1fa029db83e7c98c6bb14000000da5c15b6a8b6ed0c8b38bfeba6c10d749c044103"
    },
    "FQDN": "srvexchange2013"
}
```
To use basic remote authentication you have to set the property **UseRemote** to **true**, then you have to set **login** and **securePassword** from an account that can access the Exchange Server.

If you want to use a securePassword you have to convert your password to a secure string. Execute the comand below replacing **P@$$w0rd** with your password and put the result on the configuration file.

```
"P@$$w0rd" | ConvertTo-SecureString -AsPlainText -Force | ConvertFrom-SecureString
```

Finally you have to set the **FQDN**, FQDN is the fully qualified domain name of your Exchange server.
For more information about the FQDN format, see the Microsoft documentation [here](https://docs.microsoft.com/en-us/powershell/exchange/exchange-server/connect-to-exchange-servers-using-remote-powershell?view=exchange-ps#connect-to-a-remote-exchange-server).