# **Cryptonet**
This project focuses on developing an approach to identify cryptographic algorithms by analyzing encrypted data, using Artificial Intelligence (AI) and Machine Learning (ML) techniques.

Documentation of Results:
Cryptonet.pdf

## Data collection Source - 
https://anc.org/data/oanc/download/ <br>
There are a total of 8085 txt files from source. The available is diverse in terms of length.

## Getting the cipher texts<br>
<img width="1734" height="1125" alt="image" src="https://github.com/user-attachments/assets/2bf3fb13-364a-4c85-b90d-415926592ffd" /><br>
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
- https://drive.google.com/file/d/1xFVxq44DxGM1COcbeucTxRZMAJ5Eo20k/view?usp=sharing

### 3 methods and corresponding features<br>
<img width="477" height="293" alt="image" src="https://github.com/user-attachments/assets/6c05e118-8b19-46ce-85c6-fdf0d03aed0d" /><br>

## How each feature is extracted?
### Frequency within blocks analysis 
The method analyzes the distribution of 0s and 1s within sub-blocks of the ciphertext. It helps identify if there are any biases in the distribution of bits within the blocks. In a perfectly random ciphertext, we would expect each block to have about 50% 1s and 50% 0s. 
- Working 
   1. Divide the input sequence into ‘n’ non-overlapping blocks of ‘M’ bits.
   2. Determine the proportion of ones in each block. 
   3. Compare these proportions to the expected value of 0.5 using a chi-square test.
- Notations and assumptions
   For a sequence of length n divided into N = ⌊n/M⌋ blocks of M bits:
   - The test statistic follows a χ² distribution with N degrees of freedom. Significance alpha = 0.05
   - Calculate π_i = (ones in i-th block) / M for each block
   - Compute χ² = 4M * Σ(π_i - 0.5)² for i = 1 to N
- Example calculation
Consider the binary sequence: 1100001111000011110000111100 (n=28) and M=7 (block size)
So N=4 (Degree of freedom)<br>
<img width="428" height="277" alt="image" src="https://github.com/user-attachments/assets/5b7adc61-bcd1-4f0d-b2c7-ae7cdc931c80" /><br>
&emsp;<img width="427" height="54" alt="image" src="https://github.com/user-attachments/assets/4032b9e2-4cea-48bd-a6fb-ba3c6c085ee7" />

### Run test analysis 
This index looks at consecutive runs of the same bit (0 or 1) in the ciphertext. A run is a maximal sequence of consecutive bits of either all ones or all zeros. A higher runs index might indicate less randomness in the ciphertext, as it suggests longer stretches of the same bit. 
- Working
  1. Count the number of runs of each length.
  2. Compare these counts to the expected counts for a random sequence.
- Notations and assumptions
  For a random sequence of length n with n₁ ones and n₀ zeros:
  - Expected number of runs: e = 1 + (2n₁n₀) / n
  - Variance of the number of runs: σ² = (2n₁n₀(2n₁n₀ - n)) / (n²(n - 1))
  The test statistic is: Z = (r - e) / σ
  Where r is the observed number of runs.
- Example calculation
  Consider the binary sequence: 1011010111
  1. Count runs<br>
  <img width="230" height="150" alt="image" src="https://github.com/user-attachments/assets/fbbcb6cf-f677-4b95-b45f-c43de427c196" /><br>
  Total observed number of runs: 7
  2. Calculate expected runs: n₁ = 7, n₀ = 3, n = 10 e = 1 + (2 * 7 * 3) / 10 = 5.2
  3. Calculate variance: σ² = (2 * 7 * 3 * (2 * 7 * 3 - 10)) / (10² * 9) ≈ 1.29
  4. Calculate test statistic: Z = (7 - 5.2) / √1.29 ≈ 1.58<br>
  <img width="222" height="47" alt="image" src="https://github.com/user-attachments/assets/600a0987-fa43-4265-8a2b-676e5c8b8968" /><br>
  &emsp;<img width="217" height="107" alt="image" src="https://github.com/user-attachments/assets/01e4b055-7fed-4dde-bcf3-816f31907977" />

### Serial test analysis 
This index examines all possible sub-sequences within the ciphertext. This index helps identify patterns or biases in the sub-sequences of the ciphertext. In a truly random sequence, you'd expect each possible sub-sequence to occur with roughly equal frequency. 
- Working
  1. Count occurrences of all possible overlapping m-bit patterns. 
  2. Compare these counts to the expected counts for a random sequence.
  3. Compute test statistics based on the differences between observed and expected frequencies.
- Notations and assumptions
  For a binary sequence of length n and pattern length m:
  - Expected frequency of each m-bit pattern: n/2^m
  - Compute ψ²_m and ψ²_(m-1): ψ²_m = (2^m/n) * Σ v²_i - n, where v_i is the frequency of the i-th m-bit pattern ψ²_(m-1) is calculated similarly for (m-1)-bit patterns
  - Test statistic: ∇ψ²_m = ψ²_m - ψ²_(m-1)
  - ∇ψ²_m follows a χ² distribution with 2^(m-1) degrees of freedom. Significance alpha = 0.05
- Example calculation
   Consider the binary sequence: 0011011101 (length 10)
   Let's use m = 3 (pattern length) Degree of freedoms = 4
   1. Count 3-bit patterns<br>
   <img width="157" height="166" alt="image" src="https://github.com/user-attachments/assets/1badf4e0-9ac3-4b27-b3b6-bc0a09b944ec" /><br>
   2. Count 2-bit patterns<br>
   <img width="157" height="97" alt="image" src="https://github.com/user-attachments/assets/c7c13854-a851-49ca-b5c2-49798e8a8bba" /><br>
   3. Compute ψ²_3 = (2³/10) * (0² + 1² + 0² + 2² + 0² + 2² + 2² + 1²) - 10 ≈ 1.2
   4. Compute ψ²_2 = (2²/10) * (1² + 3² + 2² + 3²) - 10 ≈ 0.4
   5. Calculate ∇ψ²_3 = ψ²_3 - ψ²_2 ≈ 0.8
   6. Calculate p-value: p-value = 1 - CDF(χ²(4), 0.8) ≈ 0.9384<br>
   <img width="336" height="161" alt="image" src="https://github.com/user-attachments/assets/fd3fe0c8-57cd-4e58-afe7-a5e5ed0ef4eb" /><br>

## How one datapoint looks? 
Let’s say a binary cipher text is of length N. 
We have taken a block of 128 and generate 21 features as demonstrated in previous section. 
Total number of blocks = N/128 = B 
One datapoint is matrix of (B, 21)<br>
21 features<br>
<img width="630" height="1161" alt="image" src="https://github.com/user-attachments/assets/24efd3f7-297c-4234-b1bb-cebc3202be06" />

## **Why deep learning?**
In our research, we opted for a deep learning model instead of a traditional machine learning model due to the complexity and cluttered nature of the features in our dataset. With 21 features, a 3D visualization using techniques like t-SNE and PCA revealed that the feature space was highly non-linear and lacked clear separability. This level of complexity made it challenging for traditional machine learning algorithms to effectively capture the intricate patterns and relationships within the data. 

Deep learning models excel in scenarios where features are high-dimensional and non-linearly correlated, as they are capable of hierarchical feature extraction. This ability to deeply analyze and encode feature interactions is crucial for our dataset, where the underlying structure is obscured in lower dimensions.

Consequently, the deep learning model significantly outperformed traditional machine learning approaches, demonstrating its strength in understanding and leveraging the complex feature space to achieve superior performance.

## **Model architecture**
<img width="1970" height="516" alt="image" src="https://github.com/user-attachments/assets/36daffb2-b40d-45dd-a03e-7729ce02b841" /><br>

## **Analysis tools used**
<img width="1658" height="216" alt="image" src="https://github.com/user-attachments/assets/ce42a6e3-eeb9-4649-b3fe-bf7cb2e14e0d" /><br>

## 3d visualization with t-SNE
<img width="1388" height="1110" alt="image" src="https://github.com/user-attachments/assets/0ffa89a1-9c8b-45aa-be86-ba61427cfbe2" /><br>

## 3d visualization with PCA
<img width="1388" height="1110" alt="image" src="https://github.com/user-attachments/assets/53a9d112-f24f-4a35-b1dd-e81ff5938bf4" /><br>

## Exploring Test Set
<img width="1483" height="440" alt="image" src="https://github.com/user-attachments/assets/6ff47ad5-e692-4690-9f15-ea9e080b5311" /><br>

## **Evaluation results on test set**
Overall Accuracy: 88.60%<br> 
Average Confidence: 0.83
### Per-Class analysis
<img width="1507" height="437" alt="image" src="https://github.com/user-attachments/assets/e2551760-c1b2-4ad2-891c-33e435735779" /><br>
Best Validation Accuracy: 89.17%<br>
Best Epoch: 98





