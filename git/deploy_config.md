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


