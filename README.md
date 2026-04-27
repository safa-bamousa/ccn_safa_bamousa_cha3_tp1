# TP : Exploration HTTP, cURL & API REST

## TP 1 : Exploration avec les DevTools

- Quel est le code de statut ?
200 OK (La requête a été traitée avec succès)

- Quels headers de requête sont envoyés ?
```javascript
:authority
httpbin.org
:method
GET
:path
/get
:scheme
https
accept
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
accept-encoding
gzip, deflate, br, zstd
accept-language
en-GB,en-US;q=0.9,en;q=0.8
priority
u=0, i
sec-ch-ua
"Google Chrome";v="147", "Not.A/Brand";v="8", "Chromium";v="147"
sec-ch-ua-mobile
?0
sec-ch-ua-platform
"Windows"
sec-fetch-dest
document
sec-fetch-mode
navigate
sec-fetch-site
none
sec-fetch-user
?1
upgrade-insecure-requests
1
user-agent
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36
```
- Quel est le Content-Type de la réponse ?
```javascript
{
  "args": {}, 
  "headers": {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7", 
    "Accept-Encoding": "gzip, deflate, br, zstd", 
    "Accept-Language": "en-GB,en-US;q=0.9,en;q=0.8", 
    "Host": "httpbin.org", 
    "Priority": "u=0, i", 
    "Sec-Ch-Ua": "\"Google Chrome\";v=\"147\", \"Not.A/Brand\";v=\"8\", \"Chromium\";v=\"147\"", 
    "Sec-Ch-Ua-Mobile": "?0", 
    "Sec-Ch-Ua-Platform": "\"Windows\"", 
    "Sec-Fetch-Dest": "document", 
    "Sec-Fetch-Mode": "navigate", 
    "Sec-Fetch-Site": "none", 
    "Sec-Fetch-User": "?1", 
    "Upgrade-Insecure-Requests": "1", 
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36", 
    "X-Amzn-Trace-Id": "Root=1-69ef6d34-4aa5d2b402073046308b9e9e"
  }, 
  "origin": "196.70.252.213", 
  "url": "https://httpbin.org/get"
}
```

#### 1.3 Tester différentes méthodes

```javascript
// GET
fetch('https://httpbin.org/get')
  .then(r => r.json())
  .then(console.log);
```
result: 
```javascript
Promise {<pending>}
{args: {…}, headers: {…}, origin: '196.70.252.213', url: 'https://httpbin.org/get'}
args
: 
{}
headers
: 
{Accept: '*/*', Accept-Encoding: 'gzip, deflate, br, zstd', Accept-Language: 'en-GB,en-US;q=0.9,en;q=0.8', Host: 'httpbin.org', Priority: 'u=1, i', …}
origin
: 
"196.70.252.213"
url
: 
"https://httpbin.org/get"
[[Prototype]]
: 
Object
```
```javascript
// POST
fetch('https://httpbin.org/post', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'John', age: 30 })
})
  .then(r => r.json())
  .then(console.log);
```
result: 
```javascript

Promise {<pending>}
{args: {…}, data: '{"name":"John","age":30}', files: {…}, form: {…}, headers: {…}, …}
args
: 
{}
data
: 
"{\"name\":\"John\",\"age\":30}"
files
: 
{}
form
: 
{}
headers
: 
{Accept: '*/*', Accept-Encoding: 'gzip, deflate, br, zstd', Accept-Language: 'en-GB,en-US;q=0.9,en;q=0.8', Content-Length: '24', Content-Type: 'application/json', …}
json
: 
{age: 30, name: 'John'}
origin
: 
"196.70.252.213"
url
: 
"https://httpbin.org/post"
[[Prototype]]
: 
Object
```
1.4 Observer les codes de statut
Testons ces URLs et notez les codes :
https://httpbin.org/status/200  => 200 OK
https://httpbin.org/status/404  => 404 Not Found 
https://httpbin.org/status/500  => 500 Internal Server Error
https://httpbin.org/redirect/3  => 302 Found 98.XX.87.4:443

## Exercice
httpbin.org/get	
  Méthode	: GET
  Code : 200 OK
  Content-Type	: application/json
  
httpbin.org/post			
  Méthode	:POST
  Code : 405 Method Not Allowed
  Content-Type	:	text/html
  
httpbin.org/status/201	
  Méthode	: GET
  Code : 201 Created
  Content-Type	: text/html; charset=utf-8

## TP2

2.1 Requête GET simple
```bash
C:\Users\safab>curl --version
curl 8.18.0 (Windows) libcurl/8.18.0 Schannel zlib/1.3.1 WinIDN WinLDAP
Release-Date: 2026-01-07
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt pop3 pop3s smb smbs smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS HSTS HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM SPNEGO SSL SSPI threadsafe Unicode UnixSockets

C:\Users\safab>curl https://httpbin.org/get
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.18.0",
    "X-Amzn-Trace-Id": "Root=1-69ef7439-2d9dba966758c3fc12fbbfe4"
  },
  "origin": "196.70.252.214",
  "url": "https://httpbin.org/get"
}

C:\Users\safab>curl -i https://httpbin.org/get
HTTP/1.1 200 OK
Date: Mon, 27 Apr 2026 14:35:44 GMT
Content-Type: application/json
Content-Length: 256
Connection: keep-alive
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.18.0",
    "X-Amzn-Trace-Id": "Root=1-69ef7440-3e9c60ea36f3148f2aecbf63"
  },
  "origin": "196.70.252.214",
  "url": "https://httpbin.org/get"
}

C:\Users\safab>curl -v https://httpbin.org/get
* Host httpbin.org:443 was resolved.
* IPv6: (none)
* IPv4: 54.198.84.224, 3.228.76.52, 3.220.42.21, 3.234.199.80, 98.84.87.4, 100.50.202.131
*   Trying 54.198.84.224:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to httpbin.org (54.198.84.224 port 443) from 172.17.1.104 port 53876
* using HTTP/1.x
> GET /get HTTP/1.1
> Host: httpbin.org
> User-Agent: curl/8.18.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Mon, 27 Apr 2026 14:35:51 GMT
< Content-Type: application/json
< Content-Length: 256
< Connection: keep-alive
< Server: gunicorn/19.9.0
< Access-Control-Allow-Origin: *
< Access-Control-Allow-Credentials: true
<
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.18.0",
    "X-Amzn-Trace-Id": "Root=1-69ef7447-4d2de36d76a59cb8339c1a9f"
  },
  "origin": "196.70.252.214",
  "url": "https://httpbin.org/get"
}
* Connection #0 to host httpbin.org:443 left intact
```
Question : Quelle est la différence entre -i et -v ?
• -i (--include) : Affiche uniquement les headers de la réponse HTTP suivis du corps de la réponse. Cette option est pratique pour vérifier rapidement le code statut (200, 404, etc.) et les métadonnées renvoyées par le serveur.
• -v (--verbose) : Active le mode verbeux (debug). Il affiche l'intégralité du processus : la connexion réseau (DNS, TCP, TLS), les headers de la requête envoyée par votre machine, les headers de réponse reçus, ainsi que le corps. Il est utilisé pour diagnostiquer des problèmes de connexion, de certificats ou de configuration.

2.4 Suivre les redirections
```bash
C:\Users\safab>curl https://httpbin.org/redirect/3
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/relative-redirect/2">/relative-redirect/2</a>.  If not click the link.
C:\Users\safab>curl -L https://httpbin.org/redirect/3
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.18.0",
    "X-Amzn-Trace-Id": "Root=1-69ef7664-7180c39e258835cd0f3494bf"
  },
  "origin": "196.70.252.213",
  "url": "https://httpbin.org/get"
}

C:\Users\safab>
```

2.5 Télécharger un fichier
```bash
C:\Users\safab>curl -o image.png https://httpbin.org/image/png
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
  0      0   0      0   0      0      0      0                      100   8090 100   8090   0      0   9499      0                      100   8090 100   8090   0      0   8853      0                      100   8090 100   8090   0      0   8320      0                              0

C:\Users\safab>curl -O https://example.com/fichier.pdf
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
  0      0   0      0   0      0      0      0                      100    528   0    528   0      0    649      0                      100    528   0    528   0      0    602      0                      100    528   0    528   0      0    562      0                              0

C:\Users\safab>
```

Écrivez une commande cURL qui :

Envoie une requête POST à https://httpbin.org/post
Avec le header Content-Type: application/json
Avec le header X-Custom-Header: MonHeader
Avec le body {"action": "test", "value": 42}
Affiche les headers de réponse

reponce:

```bash
C:\Users\safab>curl -i -X POST -H "Content-Type: application/json" -H "X-Custom-Header: MonHeader" -d "{\"action\": \"test\", \"value\": 42}" https://httpbin.org/post
HTTP/1.1 200 OK
Date: Mon, 27 Apr 2026 14:50:49 GMT
Content-Type: application/json
Content-Length: 504
Connection: keep-alive
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

{
  "args": {},
  "data": "{\"action\": \"test\", \"value\": 42}",
  "files": {},
  "form": {},
  "headers": {
    "Accept": "*/*",
    "Content-Length": "31",
    "Content-Type": "application/json",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.18.0",
    "X-Amzn-Trace-Id": "Root=1-69ef77c9-2bd34a41747240594809d683",
    "X-Custom-Header": "MonHeader"
  },
  "json": {
    "action": "test",
    "value": 42
  },
  "origin": "196.70.252.213",
  "url": "https://httpbin.org/post"
}
```
## TP 3 : API REST avec JavaScript

Créez une fonction fetchWithRetry(url, options, maxRetries) qui :

Effectue une requête HTTP
En cas d'erreur 5xx, réessaie jusqu'à maxRetries fois
Attend 1 seconde entre chaque tentative
Retourne la réponse ou lève une erreur

```javascript
async function fetchWithRetry(url, options = {}, maxRetries = 3) {
  let lastError;

  for (let attempt = 1; attempt <= maxRetries + 1; attempt++) {
    try {
      const response = await fetch(url, options);

      // Si le statut est 5xx, on lance une erreur pour déclencher le retry
      if (response.status >= 500 && response.status < 600) {
        throw new Error(`Server error: ${response.status}`);
      }

      // Succès : on retourne la réponse
      return response;

    } catch (error) {
      lastError = error;

      // Si on a atteint le nombre max de tentatives, on arrête
      if (attempt > maxRetries) {
        console.error(`Échec après ${maxRetries} tentatives :`, error.message);
        break;
      }

      // Attendre 1 seconde avant la prochaine tentative
      console.log(`Tentative ${attempt} échouée, réessai dans 1s...`);
      await new Promise(resolve => setTimeout(resolve, 1000));
    }
  }

  // Si on sort de la boucle sans retour, on rejette la promesse
  throw lastError;
}
```

## TP 4 : Analyse des Headers de Sécurité

resultat de test des commandes:
 ```bash
C:\Users\safab>curl -I https://google.com
HTTP/1.1 301 Moved Permanently
Location: https://www.google.com/
Content-Type: text/html; charset=UTF-8
Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-2yEYYwDPCTycY4WOLT7w5Q' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
Date: Mon, 27 Apr 2026 15:01:10 GMT
Expires: Wed, 27 May 2026 15:01:10 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 220
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
```
**4.2 Analyser avec Security Headers**

Allez sur https://securityheaders.com
Entrez l'URL d'un site (ex: github.com)
Analysez le rapport
Headers:	
  checke:
    Strict-Transport-Security 
    X-Frame-Options 
    X-Content-Type-Options 
    Referrer-Policy
    Content-Security-Policy 
  Non checke:
    Permissions-Policy

**Exercice**

| Site | HSTS | X-Frame | X-Content-Type | CSP | Note |
|------|------|---------|---------------|-----|------|
| `github.com` | ✅ `max-age=31536000; includeSubdomains; preload` | ✅ `deny` | ✅ `nosniff` | ✅ `default-src 'none'` (stricte) | **A** 🟢 |
| `google.com` | ✅ `max-age=31536000` | ✅ `SAMEORIGIN` | ❌ *Missing* | ⚠️ `report-only` (non appliquée) | **C** 🟡 |
| `mozilla.org` | ✅ `max-age=31536000; includeSubDomains; preload` | ✅ `SAMEORIGIN` | ✅ `nosniff` | ✅ `default-src 'self'` | **A+** 🟢 |
