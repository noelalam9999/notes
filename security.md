# Software security
- A piece of software can be attacked to access restricted features, steal information, or execute harmful scripts.
- Any system is as secure as its weakest link.
- Monitor your processes, and use automated alerts to promptly respond to attacks

## Decryption
- Typical attacks to decode encrypted data include brute forcing and rainbow tables.
- brute forcing - trying all the possible combinations
- Rainbow tables are lists of commonly used passwords and the corresponding hashes that would result by encrypting them with popular algorithms.
  - password salting - add some random data 
- To protect you need to use longer passwords, stronger and always up-to-date algorithms, frequently update
- hash function - input and salt - bcrypt popular library
  <img alt="img.png" src="img.png"/>

## Interception
- Packet sniffing means reading the packets of data that are exchanged over a network (wifi, router, cable)
  - access payload and any data it has
- A man-in-the-middle attack happens when someone can sit in the middle of a communication between two entities and modify its content, without the parties noticing it.
  - eavesdropping - alter messages, users are unaware
- You can protect using good encryption, so even if the attacker gets access to the content they can’t read it. (HTTPS certificates)
  - serve ur data over secure network
- tempest attack - hardware attack, checking the elect signal, motion sensor of fingers, electromagnetic leakage - need to use special computer
- In the case of Internet communications this means using HTTPS and verified key certificates.
- cryptography - turn something that has meaning to a hash - only those who intend to read this will get the

## Malicious code execution
- These attacks try to execute some code on the host to obtain a certain result.
- This includes all types of code injections.
- One of them is XSS, which means cross-site scripting. This attack happens on the client-side (typically a browser), by injecting in the DOM malicious JavaScript through some user input.
- Another common attack is a SQL injection, which happens when a user tries to store some data on a SQL database which includes SQL commands.
  - delete data, obtain data
- To defend from these attacks the core principle is to never trust user input. You need to always sanitize it, by removing any characters that your system can consider as code to execute, escape user inputs, sanitize html outputs
- Also you should only use external libraries coming from trusted sources.
- Cross-site request forgery (CSRF) is a client-side attack that happens when you visit a malicious website that is sending HTTP requests to a server where you previously logged in, taking advantage of the credentials stored in your browser’s cookies.
- You can protect from CSRF using the SameSite attribute in the Set-Cookie response header. Synchroniser tokens.
- cookies - authorization and session information

## Denial of service
- Aka DoS aims at taking a system down or making it unusable.
- It works by sending a very high number of requests to a server so that the system is overloaded and becomes unavailable or crashes. 
- To defend from it you can increase the load-capability of your server, or use dedicated hardware or software that identifies the attacking IP addresses and blocks any requests from them.

## HTTPS
- Is the secure version of HTTP.
- Is based on asymmetric encryption. Each party shares a public key with the other, which uses it to encrypt any messages to be sent back. Such messages then can only be decrypted with the private key that is kept by the owner who originally sent the public key.
- SSL certificates accompany public keys to confirm the identity of a sender, which is verified by a certificate authority.
- public key - is like a lock, private key is the key that can unlock. it can also work the other way, encrypt with private key and decrypt with public key but why would you do that.
- private keys can be used as signing mechanisms - authentication token does not contain any protected content so it is ok to use private key
- website apply for SSL - websites public key is included in certificate.
  <img alt="img.png" src="img_ssl.png"/>