---
layout: page
title: End-to-End Encryption 
parent: Introduction
nav_order: 20 
---


# End-to-End Encryption 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What does it mean? 

![](https://statics.bsafes.com/endToEndEncryptionDiagram.png)
**End-to-End Encryption** means no one between Alice and Bob could know the content of their communication. In above illustration, the thick black line means encrypted data between Alice and Bob from end to end.

![](https://statics.bsafes.com/withoutEndToEndEncryptionDiagram.png)

Without End-to-End Encryption, service provider in the middle(e.g. Google, Evernote, Onenote) could know the content exchaged between Alice & Bob. In above illustration, there are 2 thick black lines,one between Alice & service provider, another one between service provider & Bob. Even though data is encrypted between Alice and service provider, likewise, encrypted between service provider and Bob, the service provider decrypts and can see the data in plain text.

Most service providers claim **Encryption at Rest**, which means they decrypt users data, process(e.g. index), then encrypt users data again before storing them in database or storage. Therefore, they know content of users data.

## How does End-to-End Encryption work in BSafes?

![](https://statics.bsafes.com/memberEncryption_v1.png)

A member creates a **member key (Km)** on the memeber's device when he or she joins a BSafes account, the key is only known by the member and is never sent to the cloud. The member's device also automatically generates a **public key (Kp)** and **private key (Kv)** pair. The device then encrypt the private key (Kv)  with the member key (Km). The **encrypted private key (eKv)**, together with the public key (Kp) are sent to BSafes server and stored in BSafes database. BSafes server does not know the member's private key, becuase BSafes server doesn't know the member key (Km) to decrypt it.

In a member's personal workspace, all pages are encrypted with the member key (Km) locally on the device. The device then send the encrypted page data to BSafes server and stored in BSafes database. Again, BSafes server does not know the page content since it doesn't have the key to decrypt.

![](https://statics.bsafes.com/teamEncryption_v1.png)

When a member (Alice) wants to collaborate with another member (Bob), Alice has to create a team first. When she creates a team, her device automatically creates a **team key (Kt)**. Then the device encrypt the team key (Kt) with Alice's member key (KmA), the **encrypted team key (eKt)** is then sent to BSafes server and stored in BSafes database. Again, BSafes server can not decrypt the encrypted team key.

For Alice, the next step is to add Bob to the team. When Alice adds Bob to the team, her device asks for Bob's public key (KpB) from BSafes server. After the device receives Bob's public key (KpB), it encrypts the team key (Kt) with Bob's public key (KpB), then the enrypted team key (eKt) is sent to BSafes server and stored in BSafes database.

For Bob to access the team, his device would ask for the encrypted team key (eKt) from BSafes server. After receiving the encrypted team key, the device then decrypt the encrypted team key (eKt) with Bob's private key (KvB) and get the team key (Kt).

All pages in a team workspace are encrypted with the team key (Kt), team members Alice and Bob now have the team key (Kt), they could edit and exchange pages with the team key. BSafes server can not decrypt the pages in a team workspace since it does not have the team key (kt). 
