# TP : Exploration HTTP, cURL & API REST

## TP 1 : Exploration avec les DevTools

- Quel est le code de statut ?
200 OK (La requête a été traitée avec succès)

- Quels headers de requête sont envoyés ?
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

- Quel est le Content-Type de la réponse ?
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


#### 1.3 Tester différentes méthodes
Utilisez l'onglet **Console** pour envoyer des requêtes :

```javascript
// GET
fetch('https://httpbin.org/get')
  .then(r => r.json())
  .then(console.log);

// POST
fetch('https://httpbin.org/post', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'John', age: 30 })
})
  .then(r => r.json())
  .then(console.log);
