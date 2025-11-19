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
# 3 Message integrity (8.3)
# 4 Authentication (8.3)
# 5 Securing e-mail (8.5)
# 6 Securing TCP connections: TLS (8.6: SSL)
# 7 Network Layer Security: IPsec (8.7)
# 8 Operational security: firewalls and IDS (8.9)