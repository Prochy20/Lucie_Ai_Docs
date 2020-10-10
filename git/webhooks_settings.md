# Nastavení webhooků

## Nastavení v GITu

Nastavení webhooku se provádí v [GITu](https://git.lucie-ai.space), kdy lze nastavit následující pole:
* Endpoint URL
* SECRET
* Content type

Doporučené nastavení:

```
EndpointURL: 'http://git.lucie-ai.space:8085/api/v1/git/'
SECRET: 'libovolny_secret_unikatni_pro_kazdy_webhook'
Content-type: 'application/www-form-urlencoded'

```


## Nastavení na DEV Serveru

Pro ověření webhooku je třeba na **DEV serveru** nastavit v mongo databázi **secret** pro vybraný **webhook**:

Kolekce: Webhooks

```
{
    "_id" : ObjectId("5f819ab84be5a0127fe0fd5c"),
    "timestamp" : ISODate("2020-10-10T11:27:52.648Z"),
    "repository" : "git@git.lucie-ai.space:Prochy20/node_test.git",
    "secret" : "QIGOFtfLTgg0pwWZJnSo5g15aoOa5Q7Rq5q6MJPGWSNWNqahYok741OFWtwKn50p2i2bxY5PJVgMVHB84y35h43LHldvXyeVRXPcRwHlnDR5jtn2xeviU9ZW",
    "__v" : 0
}

```