# Lab 1: Symmetric and Asymmetric Encryption

## Objectives

- Practice symmetric encryption and decryption using RC4 in CrypTool.
- Explore RSA encryption and decryption using an online tool.
- Install and use ccrypt in Kali Linux.
- Generate RSA keys and encrypt a text file using OpenSSL.
- Understand the difference between shared-key and public-key encryption.

## Tools

- CrypTool
- Online RSA Encryption, Decryption and Key Generator
- Kali Linux Terminal
- ccrypt
- OpenSSL

## EX1: Install CrypTool , Crypte File text by using RC4 with 32 bit Key , Next decrypt the file 

<img width="646" height="243" alt="p1 for lab1" src="https://github.com/user-attachments/assets/7140b554-77d9-46ce-90b8-e76104aa599e" />


**Explanation:** A text message was entered in CrypTool and encrypted using RC4 with the 32-bit key 12 23 56 78. The ciphertext was then decrypted using the same key, recovering the original message.

This demonstrates symmetric encryption, where the same secret key is used for encryption and decryption.

## Ex2: Using online RSA Encryption, Decryption And Key Generator Tool(Free) , click link below

https://www.devglan.com/online-tools/rsa-encryption-decryption

<img width="345" height="224" alt="p2 for lab1" src="https://github.com/user-attachments/assets/7da6391e-e6fd-4d22-a078-c2a97b1dd1e6" />


**Explanation:** The online tool was used to encrypt a text message with an RSA public key. The Base64-encoded ciphertext was then decrypted using the corresponding private key.

The decrypted output matches the original message, demonstrating asymmetric encryption with a public/private key pair.

## Ex3: Using Symmetric & Asymmetric encryption in Kali Linux

### 1) ccrypt tool ( Symmetric encryption )

<img width="552" height="540" alt="p5 for lab1" src="https://github.com/user-attachments/assets/8cfef85b-8908-43c1-a268-89733c2fceed" />


**Image explanation:** The package list was updated using sudo apt update, and ccrypt was installed using sudo apt install ccrypt. The initial misspelled command failed and was corrected.

<img width="2627" height="954" alt="p3 for lab1" src="https://github.com/user-attachments/assets/82b97c42-12c9-4996-8d13-785510c36ad4" />


**Image explanation:** The left side shows the contents of the file hackingskills before encryption. The command ccrypt -e hackingskills prompts for a password and produces hackingskills.cpt.

Displaying the encrypted file with cat produces unreadable characters because the ciphertext contains binary data.

**Clarification:** This screenshot demonstrates ccrypt encryption. It does not show decryption or recovery of the original file.

### 2) rsautl or Pkeyutl tools ( Asymmetric Encryption )

<img width="388" height="277" alt="p4 for lab1" src="https://github.com/user-attachments/assets/fd11d306-3ce6-4ded-b976-a423afcfcf26" />


**Explanation:** OpenSSL was used to generate an RSA private key, extract its public key, and encrypt a text file.

The following commands are shown:

    openssl genrsa -out private.pem 1024

Generates a 1024-bit RSA private key and saves it to private.pem.

    openssl rsa -in private.pem -out publick.pem -outform PEM -pubout

Extracts the corresponding public key and saves it to publick.pem.

    echo "ethical hacking tuition center" > net332.txt

Creates the plaintext file.

    openssl pkeyutl -encrypt -inkey publick.pem -pubin -in net332.txt -out encryption.bat

Encrypts the plaintext using the public key and saves the ciphertext to encryption.bat.

**Clarification:** Despite its .bat extension, encryption.bat contains encrypted binary data rather than a batch script. The screenshot shows encryption and ciphertext inspection, but does not show private-key decryption.

## Conclusion

The goal of this lab was to practice symmetric and asymmetric encryption using graphical, online, and command-line tools. The exercises introduced shared-key encryption, RSA key pairs, ciphertext inspection, and recovery of plaintext through decryption where demonstrated.
