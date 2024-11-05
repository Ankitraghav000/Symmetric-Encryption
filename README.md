# Symmetric-Encryption

## Project Overview
This project demonstrates the use of symmetric encryption to securely share a message file. The encryption algorithm used is AES-256.
This README provides detailed instructions for both encrypting and decrypting the message file, along with explanations for key characteristics and algorithm choice.
### Contents
#### Encryption Steps: 
Steps to generate a key and encrypt the message file.
#### Decryption Steps: 
Steps to decrypt the message file using the provided key.
#### Encryption Algorithm Details:
Information about the AES-256 encryption method and why it was chosen
### Encryption Steps
**Step 1:** Generate a Symmetric Key
To encrypt the message file, first generate a symmetric key using OpenSSL:
```
openssl rand -hex 32 > symmetric_key.key
```
**Explanation:** This command generates a random 256-bit (32-byte) key in hexadecimal format and saves it to a file named symmetric_key.key.

**Key Length:** 256 bits for AES-256, which is chosen for strong security.

**Step 2:** Create a Message File
Create a text file named message.txt with the message you want to encrypt. For example:
```
This is a confidential message intended for encryption.
```
Save this message as message.txt in the working directory.

Step 3: Encrypt the Message File
Use the generated symmetric key to encrypt message.txt using AES-256 encryption in CBC mode:
```
openssl enc -aes-256-cbc -salt -in message.txt -out encrypted_message.enc -pass file:./symmetric_key.key
```
#### Explanation:
**-aes-256-cbc:** Specifies AES encryption with a 256-bit key in CBC mode.
**-salt:** Adds random data to the encryption to make it more secure.
**-in message.txt:** Specifies the input file to encrypt.
**-out encrypted_message.enc:** Specifies the output file where the encrypted data will be saved.
**-pass file:./symmetric_key.key:** Uses the contents of symmetric_key.key as the encryption password.
After this step, you should have the following files:

- **symmetric_key.key:** The encryption key.
- **encrypted_message.enc:** The encrypted file.
## Decryption Steps
To decrypt the encrypted message, follow these steps:

**Step 1:** Verify the Key
Ensure that you have access to the symmetric_key.key file. This file is essential for decrypting the encrypted message.

**Step 2:** Decrypt the Encrypted File
Use the key and the following command to decrypt encrypted_message.enc and recover the original message:
```
openssl enc -aes-256-cbc -d -in encrypted_message.enc -out decrypted_message.txt -pass file:./symmetric_key.key
```
**Explanation:**
-aes-256-cbc: Specifies the AES encryption method in CBC mode, the same used for encryption.
-d: Indicates decryption mode.
-in encrypted_message.enc: Specifies the input encrypted file.
-out decrypted_message.txt: Specifies the output file where the decrypted message will be saved.
-pass file:./symmetric_key.key: Uses the contents of symmetric_key.key for decryption.
The decrypted message will be saved in decrypted_message.txt and should match the original message.txt.

Encryption Algorithm Details
Algorithm Used: AES-256
Key Length: 256 bits
Reason for Choosing AES-256: AES (Advanced Encryption Standard) is highly secure, widely adopted, and efficient for both hardware and software implementations. 
AES-256, with a 256-bit key, provides a high level of security suitable for protecting sensitive information.
