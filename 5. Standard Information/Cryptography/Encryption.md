#### Symmetric Encryption

Symmetric encryption, also known as secret key encryption, is a method that uses the same key to encrypt and decrypt the data. This means the sender and the receiver must have the same key to decrypt the data correctly.

If the secret key is shared or lost, the security of the data is no longer guaranteed. Critical actions for symmetric encryption methods represent the distribution, storage, and exchange of the keys. [Advanced Encryption Standard](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (`AES`) and [Data Encryption Standard](https://en.wikipedia.org/wiki/Data_Encryption_Standard) (`DES`) are examples of symmetric encryption algorithms. This type of encryption is often used to encrypt large amounts of data, such as files on a hard drive or data sent over a network. `AES` is considered to be the most secure encryption algorithm nowadays.

#### Asymmetric Encryption

Asymmetric encryption, also known as `public-key encryption`, is a method of encryption that uses two different keys:

- a `public key`
- a `private key`

The public key is used to encrypt the data, while the private key is used to decrypt the data. This means anyone can use a public key to encrypt data for someone, but only the recipient with the associated private key can decrypt the data. Examples of asymmetric encryption methods include [Rivest–Shamir–Adleman](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) (`RSA`), [Pretty Good Privacy](https://en.wikipedia.org/wiki/Pretty_Good_Privacy) (`PGP`), and [Elliptic Curve Cryptography](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) (`ECC`). Asymmetric encryption is used in a variety of applications, some of which include:

| | | 
|---|---|---|
|E-Signatures|SSL/TLS|VPNs|
|SSH|PKI|Cloud |
