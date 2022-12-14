# Konfigurace CI/CD
Konfigurace CI/CD se provádí souborem **.deploy.conf.json**, kdy tento soubor musí být obsažen v kořenovém adresáři repozitáře.

## Struktura konfiguračního souboru

Maximální verze konfiguračního souboru:

```
{

    "global": {
        "params": {
            "server": "PROD",
            "remoteDir": "/var/www/"
        }
    },

    "deploy": {
        "process": "true",
        "params": {
            "dir": "false",
            "deleteRemoteCode": "true"
        }
    },

    "install": {
        "process": "true"
    },
    

    "build": {
        "process": "true",
        "params": {
            "resultDirectory": "dist"
        }
    },

    "createDotEnv": {
        "process": "true"
    },

    "pm2stop": {
        "process": "true",
        "params": {
            "processName": "example-server"
        }
    },

    "pack": {
        "process": "true",
        "params": {
            "folder": "/"
        }
    },

    "pm2start": {
        "process": "true",
        "params": {
            "entryPoint": "./src/server.js",
            "processName": "example-server"
        }
    }

}
```

## Bloky konfiguračního souboru

### GLOBAL

Tento blok aplikuje globální nastavení CI/CD

```
    "global": {
        "params": {
            "server": "PROD",
            "remoteDir": "/var/www/"
        }
    },
```

Parametry:
* **server:** 'PROD' || 'DEV' // Výběr serveru, na který bude proveden deploy
* **remoteDi:r** '/dir' // Adresář, do kterého bude výsledný script deployován

### Deploy

Tento blok nastavuje parametry samotného deploye

```
    "deploy": {
        "process": "true",
        "params": {
            "dir": "false",
            "deleteRemoteCode": "true"
        }
    },
```

Parametry:
* **dir:** false || '/dist/' // Parametr nastavuje cestu k výslednému kódu, určenému pro deploy. Hodnota FALSE deployue celý repozitář
* **deleteRemoteCode:** true || false // Nastavením hodnoty na true bude před provedením deploye kód na cílovém serveru smazán


### Install

Tento blok provádí instalací závislostí příkazem *npm install*

```
"install": {
        "process": "true"
    },
```

### Build

Tento blok provádí build kódu příkazem *npm run build*

```
"build": {
    "process": "true",
     "params": {
        "resultDirectory": "dist"
        }
    },
```

Parametry:
* **resultDirectory** 'dir' // Slouží k označení adresáře, ve kterém se nachází výsledný kód


### Createdotenv

Tento blok vytvoří .env soubor a zapíše do něj zvolený obsah

```
"createDotEnv": {
    "process": "true"
    },
```

Obsah souboru .env se nastavuje na DEV Serveru v Mongo databázi (kolekce: dotenvs)

```
{
    "_id" : ObjectId("5f79b946405b1d14c962e08e"),
    "timestamp" : ISODate("2020-10-04T12:00:06.540Z"),
    "repository" : "git@git.lucie-ai.space:Prochy20/node_test.git",
    "content" : {
        "STEAM_USER" : "lucie_ai",
        "NODE_ENV" : "PROD"
    },
    "__v" : 0
}
```

### PM2Stop

Tento blok zastaví zvolený pm2 proces na cílovém serveru

```
    "pm2stop": {
        "process": "true",
        "params": {
            "processName": "example-server"
        }
    },
```

Parametry:
* **processName**: 'example-process' // Jméno procesu, který má být zastaven

**!** Pokud není cílový proces nalezen, deploy proces není přerušen **!**

### Pack

Tento blok vytvoří z výsledného kódu archiv .tar.gz

```
    "pack": {
        "process": "true",
        "params": {
            "folder": "/"
        }
    },
```

Parametry:
* **folder** '/' // Cílová složka, která je zabalena - celý repozitář je značen hodnotou '/'

### PM2Start

Tento blok nastartuje PM2 Process na cílovém serveru

```
    "pm2start": {
        "process": "true",
        "params": {
            "entryPoint": "./src/server.js",
            "processName": "example-server"
        }
    }
```

Parametry:
* **entryPoint** './app.js' // Entry point aplikace
* **processName** 'example-process' // Jméno pm2 procesu - toto nastavení je využíváno při dalším běhu scriptu pro adresování scriptu k zastavení

