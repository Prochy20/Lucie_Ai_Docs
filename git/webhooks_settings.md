# Nastavení webhooků

Nastavení webhooku se provádí v [GITu](https://git.lucie-ai.space)
* Endpoint URL
* SECRET
* Content type

Po nastavení webhooku v GITu je třeba do repozitáře přidat Deploy config (.deploy.conf.js) a nastavit DEV a produkční prostředí

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

### Příklad porovnání signature

```
const { payload } = req.body;
const signature = helpers.hashSecret('123456', payload);
const data = JSON.parse(payload);

const isAuthorized = req.headers['x-gogs-signature'] === signature;
```