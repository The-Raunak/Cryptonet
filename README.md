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
To get the secret key required to decrypt that data, authorized recipients publish a public key while retaining an associated private key that only they know. The sender then uses that public key and RSA to encrypt and transmit to each recipient their own secret AES key, which can be used to decrypt the data. 
Hybrid Encryption Algorithm Details: 
1. Key Sizes and Encryption Methods:
- RSA Public Key: 1024 bits (base64 encoded)
- AES Key: 128 bits (16 bytes)
- AES Mode: EAX (Encryption with Authentication)
- Encryption Type: Hybrid (Asymmetric + Symmetric)
Encryption Process:
2. a) AES Encryption:
   - Generates a random 128-bit AES key
   - Encrypts plaintext using AES-EAX mode
   - Produces:
     - Ciphertext
     - Nonce (Number used once)
     - Authentication Tag
   b) RSA Encryption:
   Converts encrypted AES key to hexadecimal string
   Encrypts the AES key using the public RSA key
3. Output Sizes:
   - AES Key: 16 bytes
   - RSA Encrypted AES Key: Approximately 128 bytes (hexadecimal representation) 
   - Nonce: 16 bytes (typical for EAX mode)
   - Authentication Tag: 16 bytes
   - Ciphertext: Same size as original plaintext
4. Block Size:
   - AES Block Size: 128 bits (16 bytes)
   - RSA Public Key Block Size: 1024 bits

### KASUMI 
Here's a concise breakdown of the Kasumi encryption algorithm implementation: 
Algorithm Overview: 
  - Type: Symmetric Block Cipher (Kasumi)
  - Origin: Used in 3G mobile communications security
- Key Characteristics: 
  1. Block Size: 64 bits (8 bytes)
  2. Key Size: 128 bits
  3. Number of Rounds: 8
- Key Generation Process:
  - Derives multiple subkeys from master key
  - Uses bit shifting and XOR operations
  - Creates 9 different key arrays:
    - KL1, KL2
    - KO1, KO2, KO3
    - KI1, KI2, KI3
- Encryption Mechanism:
  1. Key Setup:
   - Transforms master key
   - Generates multiple round-specific keys
   - Uses bit manipulation techniques
  2. Encryption Steps:
   - Splits 64-bit block into left and right halves
   - Applies 8 rounds of:
    - Function FI (substitution)
    - Function FO (Feistel network)
    - Function FL (linear transformation)
  3. Key Transformation:
   - XORs master key with predefined constant
   - Applies complex key scheduling algorithm
- Unique Features:
   - Uses two custom S-boxes (S7, S9)
   - Implements non-linear transformations
   - Provides confusion and diffusion
- Output Specifications:
   - Input: Variable length text
   - Output: Hexadecimal representation
   - Padding: PKCS7-like padding to 64-bit blocks
   - Binary conversion of hex output

### 3DES 
Encryption Algorithm Details: 
1. Key Characteristics:
   - Encryption Algorithm: Triple DES (3DES)
   - Mode of Operation: ECB (Electronic Codebook)
   - Key Length: 16 bytes (128 bits)
   - Block Size: 64 bits (8 bytes)
2. Encryption Process:
a) Key Preparation:
   - Uses a fixed key: `raunakswamy12345`
   - Key is padded to meet 3DES key requirements
b) Encryption Steps:
   - Pad input text to block size
   - Encrypt using 3DES-ECB mode
   - Convert encrypted text to hexadecimal
   - Convert hexadecimal to binary string
3. Output Sizes:
   - Key Size: 16 bytes
   - Block Size: 64 bits
   - Ciphertext: Padded to multiple of block size (< 8 bytes to 8, < 16 to 16)
   - Hexadecimal Output: Variable (depends on input text length)
   - Binary Output: Conversion of hexadecimal
4. Folder Processing:
   - Recursively finds .txt files
   - Encrypts each file individually
     
### AES
Algorithm Working:
1. The script uses AES (Advanced Encryption Standard) in ECB (Electronic Codebook) mode
to encrypt text files.
2. It walks through a specified input folder, finds all .txt files, and encrypts them.
3. Encryption process:
   - Removes trailing spaces from the plaintext
   - Pads the text to match AES block size
   - Converts the text to bytes
   - Encrypts using a fixed key
- Key Details:
   - Encryption Mode: AES-ECB (Electronic Codebook)
   - Key Size: 128 bits (16 bytes)
   - Block Size: 16 bytes (128 bits)
   - Key Used: "raunakswamy12345" (exactly 16 bytes)
- Output Characteristics:
   - Input file: Original .txt file
   - Output file: .bin file with hexadecimal encrypted content
   - Encrypted text will be larger than input due to padding
Each 16-byte block of input is encrypted independently

### ElGamal 
Here's a concise breakdown of the encryption algorithm: 
Algorithm Type: El Gamal Encryption with Custom Implementations 
- Key Generation Process: 
   - Uses SHA-256 to generate a 128-bit key
   - Generates a prime number (p) close to 2^127
   - Finds a primitive root (g) for the prime
   - Creates public key: (p, g, h)
   - Generates a private key (x)
- Encryption Mechanism:
   1. Converts input text to bytes
   2. Breaks message into blocks
   3. For each block:
   - Generates random k
   - Computes c1 = g^k mod p
   - Computes shared secret s = h^k mod p 
   - Encrypts block as c2 = (message * s) mod p
- Key Characteristics:
   - Prime (p): 128-bit
   - Primitive Root (g): Variable length
   - Public Key Components:
     - p: 128-bit prime
     - g: Primitive root
     - h: Public key element
       - Private Key (x): Derived from hash, < p-1
- Output Specifications:
   - Converts encrypted blocks to binary string
   - Output saved as .bin file
   - Binary representation of encrypted blocks
   - Output length varies with input text length
- Security Features:
   - Randomized encryption (each encryption differs)
   - Uses Miller-Rabin primality testing
   - Derives keys from input passphrase
- Unique Aspects:
   - Custom prime generation
   - Efficient primitive root finding
   - Block-based encryption approach

## Feature extraction from binary sequence 
### According to NIST we extract 21 features from 3 methods
NIST Document link : (A Statistical Test Suite for Random and Pseudorandom Number Generators for Cryptographic Applications) 
https://drive.google.com/file/d/1xFVxq44DxGM1COcbeucTxRZMAJ5Eo20k/view?usp=sharing
