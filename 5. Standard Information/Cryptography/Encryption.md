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

## Advanced Encryption Standard

Compared to DES, AES uses 128-bit (`AES-128`), 192-bit (`AES-192`), or 256-bit (`AES-256`) keys to encrypt and decrypt data. In addition, AES is faster than DES because it has a more efficient algorithm structure. This is because it can be applied to multiple data blocks at once, making it faster. This means that AES encryption and decryption can be performed faster than DES, which is especially important when large amounts of data need to be encrypted.

For example, we can find AES in many different applications and protocols, but they are not limited to:

|   |   |   |
|---|---|---|
|WLAN IEEE 802.11i|IPsec|SSH|
|VoIP|PGP|OpenSSL|


## Cipher Modes

A cipher mode refers to how a block cipher algorithm encrypts a plaintext message. A block cipher algorithm encrypts data, each using fixed-size blocks of data (usually 64 or 128 bits). A cipher mode defines how these blocks are processed and combined to encrypt a message of any length. There are several common cipher modes, including:

|**Cipher Mode**|**Description**|
|---|---|
|[Electronic Code Book](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation) (`ECB`) mode|ECB mode is generally not recommended for use due to its susceptibility to certain types of attacks. Furthermore, it does not hide data patterns efficiently. As a result, statistical analysis can reveal elements of clear-text messages, for example, in web applications.|
|[Cipher Block Chaining](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CBC) (`CBC`) mode|CBC mode is generally used to encrypt messages like disk encryption and e-mail communication. This is the default mode for AES and is also used in software like TrueCrypt, VeraCrypt, TLS, and SSL.|
|[Cipher Feedback](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_feedback_(CFB)) (`CFB`) mode|CFB mode is well suited for real-time encryption of a data stream, e.g., network communication encryption or encryption/decryption of files in transit like Public-Key Cryptography Standards (PKCS) and Microsoft's BitLocker.|
|[Output Feedback](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#OFB) (`OFB`) mode|OFB mode is also used to encrypt a data stream, e.g., to encrypt real-time communication. However, this mode is considered better for the data stream because of how the key stream is generated. We can find this mode in PKCS but also in the SSH protocol.|
|[Counter](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (`CTR`) mode|CTR mode encrypts real-time data streams AES uses, e.g., network communication, disk encryption, and other real-time scenarios where data is processed. An example of this would be IPsec or Microsoft's BitLocker.|
|[Galois/Counter](https://en.wikipedia.org/wiki/Galois/Counter_Mode) (`GCM`) mode|GCM is used in cases where confidentiality and integrity need to be protected together, such as wireless communications, VPNs, and other secure communication protocols.|