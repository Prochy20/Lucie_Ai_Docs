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