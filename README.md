# Cryptonet
This project focuses on developing an approach to identify cryptographic algorithms by analyzing encrypted data, using Artificial Intelligence (AI) and Machine Learning (ML) techniques.

Documentation of Results:
Cryptonet.pdf

## Data collection Source - 
https://anc.org/data/oanc/download/ 
There are a total of 8085 txt files from source. The available is diverse in terms of length.

## Getting the cipher texts
<img width="1734" height="1125" alt="image" src="https://github.com/user-attachments/assets/2bf3fb13-364a-4c85-b90d-415926592ffd" />
Moreover the cipher texts are converted to binary so that machine can process it.

## Technical aspects of the encryption algorithms
### RSA 
To get the secret key required to decrypt that data, authorized recipients publish a public key while retaining an associated private key that only they know. The sender then uses that public key and RSA to encrypt and transmit to each recipient their own secret AES key, which can be used to decrypt the data. Hybrid Encryption Algorithm Details: 1. Key Sizes and Encryption Methods: RSA Public Key: 1024 bits (base64 encoded) AES Key: 128 bits (16 bytes) AES Mode: EAX (Encryption with Authentication)
Cryptonet 1Encryption Type: Hybrid (Asymmetric + Symmetric)
Encryption Process: 2. a) AES Encryption: Generates a random 128-bit AES key Encrypts plaintext using AES-EAX mode Produces: - Ciphertext - Nonce (Number used once) - Authentication Tag
2. b) RSA Encryption: Converts encrypted AES key to hexadecimal string Encrypts the AES key using the public RSA key
3. Output Sizes: AES Key: 16 bytes RSA Encrypted AES Key: Approximately 128 bytes (hexadecimal representation) Nonce: 16 bytes (typical for EAX mode) Authentication Tag: 16 bytes Ciphertext: Same size as original plaintext
6. Block Size: AES Block Size: 128 bits (16 bytes) RSA Public Key Block Size: 1024 bits
