---
number headings: auto, first-level 1, max 3, 1.1
---
#uni 
# 1 What is network security (8.1)
Network security consists of:
- **confidentiality**: only the sender and the intended receiver should "understand" the message contents. This is achieved through encryption.
- **End-point authentication**: the sender and the receiver want to confirm the identity of each other.
- **message integrity**: the sender and the receiver want to ensure that message is not altered, in transit or afterwards, without detection.
- **Operational security: access and availability**: services must be accessible and available to the users.
## 1.1 Actors: Alice, Bob, Trudy
Bob and Alice want to communicate securely, but Trudy may intercept, delete and add messages. Trudy listens on the channel that Alice and Bob use to communicate.
Bob and Alice are every couple of hosts on the internet that want to communicate.
### 1.1.1 Trudy
Trudy can:
- eavesdrop: intercept messages
- insert messages
- impersonification: spoofing the source address of a packet
- hijacking: take over an ongoing connection by taking the place of either the sender or the receiver
- denial of service: prevent the service from being used by others, for example by overloading resources
# 2 Principles of cryptography (8.2)
See [[Crittografia]].
## 2.1 Language of cryptography
Alice's plaintext gets encrypted by a encryption algorithm using Alice's encryption key. The ciphertext travels through the channel and gets delivered to Bob, then gets decrypted into plaintext by a decryption algorithm using Bob's decryption key.
$$
\begin{matrix}
m: \text{ plaintext message} \\
K_A(m): \text{ ciphertext, encrypted with the key } K_A \\ 
m=K_B(K_A(m))
\end{matrix}
$$
## 2.2 Breaking encryption
There are different ways encryption can be broken depending on the information available to Trudy:
- Trudy only has the plaintext transmitted over the insecure channel, they need to decrypt it, there are two approaches to do so:
	- brute force
	- statistical analysis
- known plaintext: Trudy knows some (plaintext , ciphertext) pairs
## 2.3 Symmetric Key cryptography (8.2.1)
In Symmetric key cryptography Bob and Alice share the same key $k$ (hence "symmetric"). $K_A = K_B = K$.
Alice and Bob need to agree on the value of the key, without leaking it to third parties.
### 2.3.1 Stream ciphers
In this approach we encrypt one bit at a time.
Used for SSL/TLS connections, bluetooth connections and cellular and 4G connections.
#### Substitution cipher
Substituting letters:
- *Monoalphabetic cipher*: substitute one letter for another. here the encryption key is the mapping between letters
### 2.3.2 Block Ciphers
In this approach plaintext messages get broken into equal-size blocks, then each block gets encrypted as a unit.
#### DES: data encryption standard
This is the US encryption standard. It uses a 56-bit symmetric key and 64-bit plaintext input, it is a block cipher with cipher block chaining.
It has been brute forced in less than a day, but there is no known good analytic attack.
It gets more secure with ...
#### AES: advanced encryption standard
This is a symmetric-key NIST standard that replaced DES in November 2001.
Blocks are 128-bit wide.
Keys can be 128, 192 or 256 bit.
Brute force decryption that takes one second on DES, takes 149 trillion years on AES.
### 2.3.3 How entities establish a key
Symmetric key cryptography algorithms need the two communicating entities to establish a shared secret key.
Possible solutions are:
- **direct exchange**
- **key distribution center** (**KDC**): a trusted entity acts as an intermediary between the two entities
- **using public key cryptography** for communicating the key
#### Key distribution center
Alice and Bob know their own symmetric key ($K_{A-KDC}$ and $K_{B-KDC}$) for communicating with the KDC. This keys need to be retrieved in person at the KDC.
1. Alice sends to the KDC $K_{A-KDC}(A,B)$
2. The KDC responds with $K_{A-KDC}(R1, K_{B-KDC}(A,R1))$, now Alice knows the session key $R1$ 
3. Alice now sends Bob $K_{B-KDC}(A,R1)$, now Bob knows the session key $R1$
4. Alice and Bob communicate using the shared session key $R1$ 
## 2.4 Public Key Cryptography
Public Key cryptography uses a radically different approach: the sender and the receiver do not share the secret key, every user now has a **public** encryption key, known to all, and a **private** decryption key known only to the receiver.
Alice encrypts the plaintext with Bob's *public* key $K_B^+$, Bob decrypts the message using his *private key* $K_B^-$: $m=K_B^-(K_B^+(m))$.

Unfortunately public key cryptography is much more computationally demanding than symmetric cryptography: 100 times slower than DES.
Because of this we use public key cryptography to establish a symmetric session key.
Bob and Alice use RSA to exchange a symmetric session key $K_S$, then use $K_S$ for symmetric key cryptography communication.
### 2.4.1 Public key Cryptography algorithms
Requirements:
- $m=K_B^-(K_B^+(m))$ 
- it should be impossible to compute the private key from the given public key
another important property is the following: $K_B^-(K_B^+(m))=m=K_B^+(K_B^-(m))$.
#### RSA: Rivest, Shamir, Adleman
Nel 1977 Rivest, Shamir e Adleman propongono un sistema a chiave pubblica con funzione one-way trap-door. Turing Award 2002.
# 3 Message integrity (8.3)
Message integrity consists in allowing parties to verify that the received messages are authentic:
- the sender is who you think it is
- the contents are what the sender intended them to be
- message has not been replayed
- the sequence of the messages is maintained
## 3.1 Message digests
To implement this we introduce **message digests**: fixed-length, easy-to-compute digital footprints.
We apply a hash function $H$ to $m$ and get a fixed-size message digest $H(m)$.

Hash function properties:
- **easy to compute**
- **irreversibility**: given message digest $x$, it must be unfeasible to find $m$ such that $x=H(m)$
- **collision resistance**: given $[m,H(m)]$ it must be *computationally unfeasible* to produce $m'$ ($m' \neq m$) such that $H(m')=H(m)$.
  Si può mappare uno spazio infinito ad uno spazio finito, pur garantendo questa proprietà? Ovviamente NO ("attacco di buon compleanno"). Hence "computationally unfeasible" and not "impossible".
- **seemingly random output**
### 3.1.1 Internet checksum
The internet checksum has some of the properties of a hash function:
- fixed length output
- is many-to-one
But, given a message with its hash value, it is easy to find another message with the same hash value.
### 3.1.2 Hash function algorithms (8.3.1)
#### MD5
MD5 computes a 128-bit message digest in a 4-step process.
Given an arbitrary 128-bit string $x$, it appears difficult to find the message digest.
#### SHA-1
SHA-1 is the US standard. It produces a 160-bit message digest.
### 3.1.3 MAC: Message Authentication Code (8.3.2)
Using the MAC we can authenticate the sender and verify the message integrity. 
This approach uses no encryption and is also called "keyed hash".

We introduce a **shared secret**: a string only known to sender and receiver.
1. The sender computes the MAC of `< message , shared secret >` ($H(s,m)$).
2. the message and the MAC travel to the receiver
3. the receiver again computes the MAC of `< received message , shared secret >`, then compares it with the received MAC
4. if the two MACs are equal the message has not been altered AND the sender is the expected one.
#### Playback attack
More precisely if the two MACs correspond, we know that the MAC was *generated* by Alice, but we don't know if the `< message , MAC >` was *transmitted* by Alice.

Trudy can intercept the message, and play it back to Bob.
##### Defense
To defend from the "playback attack", we include the timestamp of generation in the message before computing the MAC. But this is quite difficult to implement, because sender and receiver clock may not be synchronized. The real solution is using **OTP** (one time password).

1. Alice contacts Bob
2. Bob sends an OTP $R$
3. Alice computes the MAC as follows: $\text{MAC}=H(R,s,m)$
4. Bob expects ONE message PER sent OTP
## 3.2 Digital signatures (8.3.3)
Digital signatures are a cryptographic technique that allows the sender to digitally sign a document.
A digital signature is:
- **verifiable**: the recipient can verify and prove that the sender and no one else signed the document
- **non-forgeable** 
And allows:
- **non repudiation**: the recipient can prove that the sender signed it
- **message integrity**

> MAC cannot be used as a digital signature because the secret is *shared* between the two communicating.

For authentication we use asymmetric cryptography ([[#2.4 Public Key Cryptography]]):
1. Bob signs $m$ by encrypting with his private key $K_B^-$ 
2. Bob sends the signed message $K^-_B(m)$
3. Alice can verify that the sender is Bob if the message can be decrypted with Bob's public key $K_B^+$ 

But as we said asymmetric cryptography is computationally demanding, so we sign the digest, not the message (the message can be arbitrarily long!):
1. Bob computes the digest: $H(m)$
2. Bob signes (encrypts) the digest with its private key
3. Bob sends the message $m$ with the encrypted message digest $K^-_B(H(m))$
4. Alice computes the digest of the received message: $H(m)$ 
5. Alice decrypts the received digest using Bob's public key and obtains (hopefully) the message digest $H'(m)$
6. Alice compares $H(m)$ and the decrypted messages digest $H'(m)$, if they are equal the message and the sender can be trusted.
### 3.2.1 CA: public key certification authorities
Who guarantees that Alice actually has Bob's public key?
A **certification authority** (**CA**) binds a public key to a particular entity $E$.
The entity $E$ registers its public key with the CA, providing a "proof of identity".
1. The CA creates a certificate binding the identity of $E$ to $E$'s public key
2. the certificate gets digitally signed by the CA using the CA's private key
3. when Alice wants to ensure Bob's identity, it decrypts the certificate using the CA's public key
The CA's public key is supposed to be known by everyone.
# 4 Authentication (8.3)
Goal: Bob wants Alice to prove her identity to him.
## 4.1 AP: Authentication Protocol
- AP1.0: "I am Alice"
- AP2.0: Alice says "I am Alice and this is my IP address"
- AP3.0: "I am Alice" and sends her secret password to prove it and sends her IP address (Trudy listens to the password the first time and then copies it)
- AP3.1: AP3.0 with encrypted password (Trudy can still paste the encrypted password)
- AP4.0: Bob sends Alice a **nonce** $R$, Alice must return $R$ encrypted with the shared secret key. Now Bob knows Alice is *live*. Requires a shared symmetric key.
- AP5.0: AP4.0 but using public key cryptography:
	1. -> I am Alice
	2. <- R
	3. -> $K_A^-(R)$
	4. <- send me your public key
	5. -> $K_A^+(R)$
	This protocol is susceptible to "man in the middle" attacks, when Alice sends "I am Alice", Trudy can intercept it and send it herself, now Bob will send Truly the **nonce** 
# 5 Securing e-mail (8.5)
For securing e-mail we need both **Authentication** and **message integrity**.
We use **PGP** (**pretty good privacy**).
## 5.1 E-Mail authentication
Alice wants to send *confidential* e-mail $m$ to Bob:

Alice:
1. generates a random symmetric private key, $K_S$ 
2. encrypts message with $K_S$ (for efficiency)
3. also encrypts $K_S$ with Bob's public key
4. sends both $K_S(m)$ and $K^+_B(m)$ to Bob

Bob: 
1. uses his private key to decrypt and recover $K_S$
2. uses $K_S$ to decrypt $K_S(m)$ and obtains $m$ 
## 5.2 E-Mail Authentication and Message Integrity
Alice digitally signs the hash of her message with her private key, providing both integrity and authentication.
## 5.3 E-Mail Authentication, Integrity and Confidentiality
![[Pasted image 20251126160543.png]]
# 6 Securing TCP connections: TLS (8.6: SSL)
# 7 Network Layer Security: IPsec (8.7)
# 8 Operational security: firewalls and IDS (8.9)