# Networking

## Protocols
- Are needed for two entities to communicate with each other.
- Standardize how communication starts and ends, and how information is passed.
  - data formats, address formats, routing, acknowledgements and errors
  - layering
- The Internet is a protocol, that allows to link billions of devices worldwide.

## IP addresses (internet protocol address), ports, LAN and WAN 
- An IP address in a computer network is a unique identifier, that allows devices to find each other.
- The standard has evolved from IPv4 (32-bit) to IPv6 (128-bit).
- The IP address is followed by a network port, that defines what process you’re interacting with. The TCP-UDP protocol provides 65535 network ports (the first 1023 are reserved for the operating system).
- LAN means “local area network” and refers to the “internal network” (e.g. an office).
  - each device has its own private IP address
- WAN means “wide area network” and refers to the “external network” (e.g. the Internet).
- any communication between LAN and WAN happens through gateway - LAN is a protected safeplace

## Data serialization and transport
- Data to be transmitted need to be serialized first (i.e. converted to binary).
- This is done using electricity or light (optical)
- Transmission of data happens in small `packets`, which are then recomposed on the other side, as this allows for better error handling. Just retransmit this packed instead of from the beginning.

## URI, URL, and DNS
- URI means “uniform resource identifier”, in the Internet this corresponds to a URL (i.e. “uniform resource locator”).
- A generic URI is of the form: `scheme://host[:port]/path[?query][#fragment]`.
- A URL to be valid needs to have a scheme, host, port (if omitted is 80 by default), and path. Queries and fragments are optional, and used on a need basis.
  - query start with ? and are key value pairs with =
  - fragments start with # for information only used in the browser
- DNS means “domain name system”, and is a distributed database of name servers spread across the Internet with the responsibility of converting domain names into their corresponding IP addresses, so that each request can reach the correct destination.
  - each name server is like an address book
  - when browser sends out a request, goes to the dns, gets the IP address and then reaches that IP address

## HTTP(s) and status codes
- HTTP means “hypertext transfer protocol” and is the foundation of data communication for the world wide web.
- It functions as a request-response protocol in the client-server computing model, and is “stateless” (i.e. each request is completely independent from the others).
- HTTPS is a safer variant of HTTP, where the connection is encrypted.
- Every communications starts with a request with a client, the server cannot initiate communication, only reacts to the request with responds
- each request is unique, since they are stateless they cannot remember each other
- Every request and response comes with “headers” (meta info), and can include a “body” (payload).
- HTTP provides a pre-defined set of request methods, which are indicated in the headers. The main ones are: GET, POST, PUT, DELETE.
- GET is a “safe” method (it doesn’t modify resources on the server).
- GET, PUT, and DELETE are “idempotent” (repeating them “n” times doesn’t change the final result on the server).
- Each server response has a “status code” in its headers. Status codes are divided in the following ranges:
  - 1xx informational (hold on)
  - 2xx success (here you go)
  - 3xx redirection (go away)
  - 4xx client error (you f*cked up)
  - 5xx server error (I f*cked up)
  
## Ajax and CORS
- Ajax is a way to make asynchronous HTTP requests through JavaScript (i.e. without having to reload the entire page).
```javascript
// Browser API
const httpRequest = new XMLHttpRequest();
httpRequest.onreadystatechange = cb;
httpRequest.open('GET', '/weather');
httpRequest.send();
```
```javascript
// jQuery
$.get('/weather', cb);
```
- Because Ajax can use any HTTP method (thus performing potentially harmful requests), it’s been limited to the “same origin” policy. By default browser only allows only AJAX request to the same domain where the request originated from.
- Eventually CORS (i.e. “cross-origin resource sharing”) has been introduced to the HTTP standard, so that each domain can define whether to accept asynchronous requests from other domains (through the `Access-Control-Allow-Origin header`).

## WebSockets and WebRTC
- Other communication protocols exist outside of HTTP (e.g. ftp, mail, etc).
- WebSockets is a stateful protocol, that allows the server to send “events” back to the client, after an initial “handshake” connection has been established, and until it’s terminated by either side.
- a real time behaviour can be simulated with all link - client sends request to server to check if there is anything new
- WebRTC is a recent protocol, that allows clients to directly establish a peer-to-peer connection between them and share a data stream without passing through a server (e.g. audio, video, files, etc).
  - content transmitted does not get stored to third party server - security
