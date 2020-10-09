# Webhooks
## Příchozí webhook

Gogs GIT může poslat na vybranou adresu webhook metodou **POST** obsahující informace o provedené akci

### Příklad:

**Headers**
```
Request URL: https://99e2a0f235a5.ngrok.io/git
Request method: POST
X-Github-Delivery: 9c131057-84a8-45c0-9c91-d661c2c9115c
X-Github-Event: push
X-Gogs-Delivery: 9c131057-84a8-45c0-9c91-d661c2c9115c
X-Gogs-Event: push
X-Gogs-Signature: 1b2b02f4a34608e00f9bd099a006da812d00bffa68e4b291e4e17445bd09f013
```
**Payload**
```
{
  "ref": "refs/heads/master",
  "before": "6abb4a728c8c4bfcb34ee7ffdb47f7ad1e98f487",
  "after": "6abb4a728c8c4bfcb34ee7ffdb47f7ad1e98f487",
  "compare_url": "",
  "commits": [
    {
      "id": "6abb4a728c8c4bfcb34ee7ffdb47f7ad1e98f487",
      "message": "dalsi push do repository\n",
      "url": "https://git.lucie-ai.space/Prochy20/node_test/commit/6abb4a728c8c4bfcb34ee7ffdb47f7ad1e98f487",
      "author": {
        "name": "Prochy20",
        "email": "prochy.20.m@seznam.cz",
        "username": "Prochy20"
      },
      "committer": {
        "name": "Prochy20",
        "email": "prochy.20.m@seznam.cz",
        "username": "Prochy20"
      },
      "added": null,
      "removed": null,
      "modified": [
        "src/server.js"
      ],
      "timestamp": "0001-01-01T00:00:00Z"
    }
  ],
  "repository": {
    "id": 10,
    "owner": {
      "id": 1,
      "username": "Prochy20",
      "login": "Prochy20",
      "full_name": "Prochy 'EM",
      "email": "prochy.20.m@seznam.cz",
      "avatar_url": "https://secure.gravatar.com/avatar/fe632ef8ac4b66440a7e602fd88a675f?d=identicon"
    },
    "name": "node_test",
    "full_name": "Prochy20/node_test",
    "description": "",
    "private": true,
    "fork": false,
    "parent": null,
    "empty": false,
    "mirror": false,
    "size": 262144,
    "html_url": "https://git.lucie-ai.space/Prochy20/node_test",
    "ssh_url": "git@git.lucie-ai.space:Prochy20/node_test.git",
    "clone_url": "https://git.lucie-ai.space/Prochy20/node_test.git",
    "website": "",
    "stars_count": 0,
    "forks_count": 0,
    "watchers_count": 1,
    "open_issues_count": 0,
    "default_branch": "master",
    "created_at": "2020-10-03T23:20:40Z",
    "updated_at": "2020-10-07T19:51:28Z"
  },
  "pusher": {
    "id": 1,
    "username": "Prochy20",
    "login": "Prochy20",
    "full_name": "Prochy 'EM",
    "email": "prochy.20.m@seznam.cz",
    "avatar_url": "https://secure.gravatar.com/avatar/fe632ef8ac4b66440a7e602fd88a675f?d=identicon"
  },
  "sender": {
    "id": 1,
    "username": "Prochy20",
    "login": "Prochy20",
    "full_name": "Prochy 'EM",
    "email": "prochy.20.m@seznam.cz",
    "avatar_url": "https://secure.gravatar.com/avatar/fe632ef8ac4b66440a7e602fd88a675f?d=identicon"
  }
}
```

## Nastavení

Webhooku lze nastavit 
* Endpoint URL
* SECRET
* Content type


## Ověření webhooku

Pro ověření se používá HASH obsažený v hlavičce 

```
X-Gogs-Signature: 1b2b02f4a34608e00f9bd099a006da812d00bffa68e4b291e4e17445bd09f013
```

Hash je vytvořen z **PAYLOAD** funkcí SHA256 HMAC hex digest, při použití zadaného **SECRET**

Pro úspešné vypočítání hashe na straně serveru je třeba nastavit **Content type**
```
application/x-www-form-urlencoded
```

### Příklad porovnání signature

```
const { payload } = req.body;
const signature = helpers.hashSecret('123456', payload);
const data = JSON.parse(payload);

const isAuthorized = req.headers['x-gogs-signature'] === signature;
```