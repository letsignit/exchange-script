# Filter EmailAddresses

This sample show you how to make a filter on mailbox email.

```
"Exchange": {
    "Filter":"EmailAddresses -like '*@domain.com'",
    "UseRemote":false
}
```
In this example below you get all mailboxes that have an email containing '@domain.com'