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

Exercice
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

**Exercices**

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
