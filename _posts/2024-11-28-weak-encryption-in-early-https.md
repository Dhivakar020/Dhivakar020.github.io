---
title: "HTTPS: When ‘S’ Stood for ‘Sorta Secure’"
date: 2024-11-28 10:00:00 +0000
categories: Browsers-are-weird
tags: [browsers, vulnerabilities, cryptography]
excerpt: "Weak Encryption in Early HTTPS"
---

---

> My write-up can be subjective. I understand that not everyone will necessarily agree with my points. Please don’t waste your time trying to prove me wrong, but if you see something really wrong, feel free to let me know.
> {: .prompt-warning }

---

## Introduction

Early browsers really lacked standards to provide confidentiality in communications.
It is really surprising to know that HTTP by default is insecure. It just transmits plaintext data.
The whole web was mainly unencrypted and sensitive data such as passwords, and session cookies were transmitted as plain text, which makes them vulnerable to MITM and sniffing attacks. In this write-up, i am not going to explain what is MITM, sniffing nor about the tools used for exploits. Rather i am focusing on how the browsers evolution affected the confidentiality and how different technologies, protocols were introduced to provide confidence in communication.

## Early Days of the Web (1990s),

- Early browsers like Netscape Navigator (1994) and Internet Explorer (1995) did not have any security mechanism to tackle attack against confidentiality. This means that HTTP exchanged data in the form of plain text, which could be easily intercepted by attackers in the same network(insiders).
- Early history of MITM attacks were said to be carried out using ethernet sniffers because WLANs were not standardized until 1997 by IEEE 802.11.

## The Introduction of SSL/TLS (Mid-1990s),

- Netscape Navigator (1995) was said to be one of the first browsers to support SSL(Secure Socket Layer). This SSL protocol was designed to focus on encrypting data transmitted between client and server to prevent sniffing and MITM attacks.
- However, this protocol was not robust against every attacks which is why it continued to evolve resulting in TLS version-1.3 today.
- Every version of SSL was deprecated at certain point in the past and was replaced by some other versions.
- In short, Refer [SSL evolution](https://beaglesecurity.com/blog/article/importance-of-tls-1-3-ssl-and-tls-vulnerabilities.html)

| SSL version | Published | Deprecated |
| ----------- | --------- | ---------- |
| SSL 2.0     | 1995      | 2011       |
| SSL 3.0     | 1996      | 2015       |
| TLS 1.0     | 1999      | 2020       |
| TLS 1.1     | 2006      | 2020       |
| TLS 1.2     | 2008      | still used |
| TLS 1.3     | 2018      | still used |

## Weakness in SSL 2.0 and 3.0,

Early versions of SSL had flaws like **weak encryption algorithms** and **vulnerabilities in the protocol itself.** Attackers used these weaknesses to not only for interception but also for modification. This compromises both confidentiality and integrity. Tools like SSLStrip (2009), were used to downgrade HTTPS to unencrypted HTTP.
Refer [SoK: SSL and HTTPS:](https://www.ieee-security.org/TC/SP2013/papers/4977a511.pdf)

1. **Weaknesses in Cryptographic Primitives**,
   - **Weak Encryption & Signature Key Lengths**: Any symmetric key encryption scheme with 40, 56, or 64 bit keys is subject to a brute-force attack.
   - **Weak Hash Functions**.
2. **Implementation Flaws and Related Attacks**,
   - **PRNG Seeding**: The Netscape browser (prior to 1.22) relied on a PRNG implementation with weak keys allowing the TLS session key (master secret) to be predictable. Recently, 0.5% of TLS certificates were found to have recoverable RSA private keys due to shared prime factors
   - **Remote Timing Attacks**: Remote timing attacks have been used against TLS servers that use an optimized variant of RSA decryption, the default in OpenSSL versions prior to 0.9.

## Modern HTTPS & Continued Risks (2000s - Present),

#### HTTPS Adoption

- Major browsers started enforcing HTTPS on websites. Google Chrome and Mozilla Firefox labeled non-HTTPS sites "Not Secure" to pressure users into adopting encryption.
- The HSTS header, which was first seen in 2009, would enable websites to enforce https by default and prevent some of the MITM attacks by the attackers.

#### Still Vulnerable to Advanced MITM Attacks,

Even though HTTPS is now more widely implemented, sophisticated forms of MITM attacks are still feasible:

- Certificate Impersonation: An attacker could use a compromised CA or issue rogue certificates for websites so that he could masquerade as secure websites and intercept encrypted traffic.
- SSL/TLS Weaknesses: Even the latest versions of SSL/TLS have been found vulnerable periodically: for example, Heartbleed (2014), which was a vulnerability used for stealing private keys from or extracting plaintext data from vulnerable servers.

#### Preventative Features in Browsers to Avoid MITM Attack

- The modern versions of browsers rely on certificates pining and public keys pinning. The server is legitimated to make such attack even more difficult, almost impossible.
- Content Security Policy (CSP) headers and other more advanced web security features assist in defending against such attacks as script injection, which might be deployed in MITM scenarios.

## Why is TLS/SSL specific to transport layer?

1. **Process-to-Process Communication**:
   - it secures communication between **specific processes or applications** running on different machines.
   - SSL/TLS works on top of transport protocols like TCP to ensure that data exchanged between these processes is secure, regardless of the type of application (HTTP, FTP, etc.) being used.
2. Independence from Application Layer:
   - Since SSL/TLS operates at the transport layer, it secures all data sent between two processes, making it **transparent to the applications**.
   - Applications will not need to worry about security because SSL/TLS handles it for them.

#### Working of modern TLS,

- I don't want to explain TLS in detail and make it like a lecture. So, i will try to explain as short as possible. If you need detailed explanation refer [IETF RFC 8446](https://datatracker.ietf.org/doc/html/rfc8446) for detailed explanation.

1. The TCP Handshake,
   - The client and server makes a TCP handshake to establish connection.
2. Certificate verification,
   - The server sends a certificate that contains a lot of things from which one of them is a Public key.
   - Remember when there are two keys (public and private) involved in an encryption, it is asymmetric and the algorithm is computationally expensive.
   - Also a plaintext encrypted by a public key can only be decrypted using it's adjacent private key and vice versa.
3. Key Exchange,
   - The client then generates a session-key which later will be used for encrypting and decrypting the plaintext data that is going to be transmitted between client and server using HTTP.
   - The problem arises when the client wants to share this session-key to the server without losing its confidentiality.
   - This is where the client uses the public-key received from the certificate to encrypt the session-key.
   - This encrypted key will be shared to server.
   - This is the best way to exchange the session-key because only the server has the adjacent private-key to decrypt the message from client.
   - In this way, the confidentiality is still maintained
4. Data Transfer,
   - By now, both server and client will have a common session key which can be used for encryption purposes.
   - One might ask why can't Asymmetric encryption algorithms like RSA be used for communication as it won't need the Key exchange mechanism.
   - The answer is very simple because Asymmetric encryption algorithms are computationally expensive which cannot be used for encrypting every single message transmitted between the client and server.

## Conclusion,

The earliest recorded MITM and sniffing attacks in web browsers took place as soon as web traffic began to be transmitted in plaintext (1990s). With the introduction of SSL and HTTPS, these attacks became more difficult but not impossible. Early SSL weaknesses and tools like **SSLStrip** and **Firesheep** showed how MITM and sniffing attacks could still occur, especially over unsecured networks. Modern browsers now use **HTTPS**, **HSTS**, and other security protocols to defend against these attacks, but vulnerabilities and sophisticated techniques still pose a risk, especially if attackers can exploit weaknesses in encryption or certificate management.
