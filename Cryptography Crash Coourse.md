---
title: Cryptography Crash Coourse
tags: [Notebooks/HackerOne]
---

# Cryptography Crash Coourse
## Intro
### XOR

A  | B  | R
--- |--- |---
1 | 1 | 0
1 | 0 | 1
0 | 1 | 1
0 | 0 | 0

XOR is important for crypto because it is reversable

Given : 
* **D = A ^ B**
* **A = D ^ B**
* **B = D ^ A**

XOR is used for One time pad constructs : You use a key to xor a plaintext once. 

You can then decrypt using the same key.

But how to pass the key to th relevant parties ? Cryptography tries to answer that question.

Two families of ciphers :

* Symmetric : Both side share same key
  * Stream : Encrypt data byte per byte
  * Block : Encrypt data block by block
* Asymmetric : Each side has their own private key and exchange public keys
## Symmetric Ciphers

### Stream ciphers

Most common one is RC4, found in SSL. Same method to encrypt and decrypt : XOR plaintext with the key to get ciphertext, and XOR ciphertext with the key to get plaintext.

### Block ciphers

In a block cipher, you split your data into N-byte blocks and encrypt them separately. Usage of padding to complete blocks. The encryption and decryption processes are not the same. There are two main modes : ECB mode and CBC mode.

#### ECB Mode
![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d6/ECB_encryption.svg/1202px-ECB_encryption.svg.png)

Electronic CodeBook mode is the simplest mode of operation 
for a block cipher : each plaintext block is encrypted independently. If you see 2 identical cyphertext block it means they have the same plaintext.

#### CBC Mode
![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/CBC_encryption.svg/1202px-CBC_encryption.svg.png)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2a/CBC_decryption.svg/1202px-CBC_decryption.svg.png)
In Cipher-Block Chaining (the most common form), each plaintext block is XORed with the ciphertext of the previous block before encryption, The opposite is performed for decryption. The first block is XORed with an Initialisation Vector (IV).

Because blocks are chained this way, **flipping one bit of ciphertext in block 0 will flip the same bit of plaintext upon decryption** this can cause bugs.

## Asymmetric ciphers

Each party has a public and private key (RSA is an asymmetric cipher). AC are used for encryption and signing (process that allows to validate the source of a message).

AC are often used to securely transmit symmetric keys. 

## Hashes 

Takes in an arbitrary blob of data and generates a fixed sized output (128-512 bits). Multiple inputs can generate the same output but it is really hard to find that kind of collision.

Hashes are useful to determine the integrity of data.

## MACs

Message authentication codes are based on hashes. But you have a shared key to generate and validate the mac. Most famous one is HMAC :

`HMAC(key, message) = hash(key + hash(key + Message))`
