# Lab 4: Building Cryptographic Tools with Python (closeSSL Project) 💻🔒

**Name**: syed 

**Student ID**: NWS23010037

## Lab Objective 💪

In this lab, we’re diving into coding our own cryptographic toolkit called `closeSSL` using Python! We’ll implement key cryptographic operations, including:

- **Symmetric Encryption** with AES-256-CBC
- **Asymmetric Encryption** with RSA (2048-bit)
- **Hashing** with SHA-256
- **Digital Signatures** with RSA and PSS padding

By the end of this lab, you’ll be able to:
- Encrypt and decrypt files using AES and RSA.
- Generate and verify SHA-256 hashes for data integrity.
- Sign and verify files with digital signatures.


**Let’s get coding!** 🚀

---

## Tools Used 🛠️

 **Python 3** with libraries:
   - `pycryptodome` (for AES and RSA)
   - `cryptography` (for digital signatures)
   - `prompt_toolkit` (for interactive file input)
   - `tabulate` (for pretty hash output)


---

- **banners/**: ASCII art for each module’s interface.
- **modules/**: Python scripts for each crypto operation.
- **main.py**: closessl a menu-driven interface.

---

## closeSSL Project Overview 

`closeSSL` is our custom Python-based cryptographic toolkit. It integrates AES, RSA, SHA-256, and digital signatures into a single command-line app. The `main.py` script launches a menu where you can choose tasks, and each module uses `prompt_toolkit` for  file path input with autocompletion. 

### Running closeSSL
```bash
pip install pycryptodome cryptography prompt_toolkit tabulate
python main.py
```

This installs dependencies and fires up the `closeSSL` menu. 

---

## **Task 1: Symmetric Encryption using AES** 🔐

**Objective**: Encrypt and decrypt a file using AES-256-CBC. We’ll encrypt a message  and decrypt it safely.

### Steps 🚶‍♂️

#### 1. Create a Sample Text File
Create a file with your message.

**Command** (in terminal, outside closeSSL):
```bash
echo "Hi adam syed nak kopi" > message.txt
```

**Example**:
```bash
┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat syed_message.txt 
hi adam syed nak kopi
```

#### 2. Run closeSSL and Encrypt
Launch `closeSSL`, select AES encryption, and generate a key and IV.

**Command**:
```bash
python main.py
```

**Steps in closeSSL**:
- Choose **1. AES Encryption**.
- Enter `n` to generate a new 256-bit key and 128-bit IV.
- Save key to `key.txt` and IV to `iv.txt`.
- Enter `syed_message.txt` as the input file.
- Save encrypted output as `aes.enc`.

**Example Output** (from `aes_encryption.py`):
```
█████╗ ███████╗███████╗      ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔════╝      ██╔════╝████╗  ██║██╔════╝                              
███████║█████╗  ███████╗█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██║██╔══╝  ╚════██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████╗███████║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚══════╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
=================== [Disclaimer: This tools for aes-256-cbc only] =====================


Enter key file path or press `n` to generate key: n

[+] Generated Key (hex): 439f4e4be9ebca09686fa5dd2a237df01ab630e94a196def02be03b9d8184839
Save key as: key.txt
[+] Saved to key.txt

[+] Generated IV (hex): 81b7d6b37e6ffa491bd5fee829533ed7
Save IV as: iv.txt
[+] Saved to iv.txt
 
Enter file path to encrypt: syed_message.txt
Save encrypted file as: aes.enc
[+] Saved to aes.enc
[+] Done. Press Enter to continue...


```

#### 3. Decrypt the File
Use `closeSSL` to decrypt the encrypted file.

**Steps in closeSSL**:
- Choose **1. AES Encryption**, then **2. Decryption**.
- Enter `key.txt` and `iv.txt` paths.
- Enter `aes.enc` as the input file.
- Save decrypted output as `aes.dec`.

**Example Output**:
```
█████╗ ███████╗███████╗      ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔════╝      ██╔════╝████╗  ██║██╔════╝                              
███████║█████╗  ███████╗█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██║██╔══╝  ╚════██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████╗███████║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚══════╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
=================== [Disclaimer: This tools for aes-256-cbc only] =====================


1. Encryption
2. Decryption
q. Exit
Select option: 2
Enter key file path: key.txt
Enter IV file path: iv.txt
Enter file path to decrypt: aes.enc
Save decrypted file as: aes.dec
[+] Saved to aes.dec
[+] Done. Press Enter to continue...


```

#### 4. Verify the Decrypted Content
Check if the decrypted file matches the original.

**Command**:
```bash
cat aes.dec
diff aes.dec syed_message.txt
```

**Example**:
```bash

 █████╗ ███████╗███████╗      ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔════╝      ██╔════╝████╗  ██║██╔════╝                              
███████║█████╗  ███████╗█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██║██╔══╝  ╚════██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████╗███████║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚══════╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
=================== [Disclaimer: This tools for aes-256-cbc only] =====================


1. Encryption
2. Decryption
q. Exit
Select option: q
[+] Exiting. Bye!

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat aes.dec 
hi adam syed nak kopi

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat syed_message.txt 
hi adam syed nak kopi

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ diff syed_message.txt aes.dec 

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ 


```

*No output from `diff` means they match! 🎉*



### Analysis 🧠
- **How It Works**: `aes_encryption.py` uses `pycryptodome` for AES-256-CBC with PKCS7 padding. The IV ensures unique ciphertexts.
- **Security**: Strong as long as the key is secret.
- **Real-World Use**: AES secures HTTPS and VPNs.

---

## **Task 2: Asymmetric Encryption with RSA** 🔑

**Objective**: Generate an RSA key pair, encrypt a short message, and decrypt it.

**Full Source Code**: 📄 [rsa_encryption.py](modules/rsa_encryption.py)

### Steps 🚶‍♂️

#### 1. Generate RSA Key Pair
use closeSSL to generate a 2048-bit RSA key pair.

**Command**:
```bash
python3 main.py
```

**Steps in closeSSL**:
- Select **2. RSA Encryption**, then **3. Generate RSA Keys**.
- Save private key as `private.key`.
- Save public key as `public.key`.

**example**:

```bash

██████╗ ███████╗ █████╗       ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔══██╗      ██╔════╝████╗  ██║██╔════╝                              
██████╔╝███████╗███████║█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██╗╚════██║██╔══██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████║██║  ██║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
==================== [Disclaimer: This tools for RSA 2048 bits] ======================


1. Encryption
2. Decryption
3. Generate RSA Keys
q. Exit
Select option: 3
[+] Private Key:
 -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAking7w3RhI8t60TL+WTulsDQ2VUwuiaijDn9/8nIHrX3PIOF
aaYfxZFnxbR6L7bS3dJJg8txiMiffcTGgyqw23X0haiQ1wiGPjMPxtjqsb8tZK2X
8+DEXEVXP4JuLwnQ7CpHwTNOfkaOtqSocrXgo+AGn5WBIZL6fMQyn2RY6SS5hngx
DPtcyKZpIIAtgr4Lh7oLRixtEltqKO/4aggO3BK9NOBx2SjvaJviXMcUErLME1nV
mGexklsCJj+w1e3pwL8rSVfVU4KYBcgvI64U3I52XQWA+pDwCSHG5iZ3cG5mVooS
XLvLg/RslHeYw8EMVF6Z++7k+UDhvLkwUhzTSwIDAQABAoIBAAFhmpnnvDElK+lA
mdozf/sLZhiHsObcHUZ3TdUwUk8n/RF5/2AY4nf61cuNLGfDBzRyxksT4xtzJJQL
BgKQprc24tFYicszw2usY9vHNQCVA+14Tn/5gcw1bjZQGeZ2kJ41ZWmH/e085ssH
Ef3I249GO18gCeZdUzdWoKaCS5d4bmFwo04sQlAmGbHbWSdY+zI1dqfu5+idvq8i
BuXy68ovmTRZ8xFMdser4jtBbhYwL/ARMUxUH/XXfAAX66UM8aNOHBUtyYfCTjXA
W4sk3T8zpZ+dfRDUkyNaQCL9dJHvICTxq3z7LKZKL0s5/Zm/JFrBU10/Hi2c+VlW
GZBdCUECgYEAtjHLMxSR6rcAIHjYzwgRvxfgPNurc06HJRJ0PRhIZ7liB1+YQjrm
W36/NeE+w+zymXp1ATVTgRUbBxH9jkD4AhIpPntBGF4b6VgoFu64H8SJ6Up/UDwx
py2eFO6+hBfPE91Uty5SrEGKWAGf3CuQuz6YnCDg6C1AkL7fSn/VLbECgYEAzV+N
i40fHiDpCQRdGZNrClxJ4SDVXSp7jTLZIqqOKL6jLxo/VSFY3bWBgHjqr6aaHhmq
rBOt1deW2VvwH/nZg0X5qDU0NL3OCDafSKMErSTgHGVJAlEfF0kqn4q5+ak2kzPX
wszcvI2TCT5DsSEc/EDkzjjStAVkxoeWAx2JY7sCgYAOqW8qyyr68oMmGdOIxaN3
91nqS9s+SkGB8Dw+dmfNQRPsd/ruyYKkNkz47wl4Bud3Bm3IDRyNNL+aEA6RlhTf
Rcrf5ldUuK4SVy/SuJ9EnzJh/cbFFDMCux8PnC7kvm3BsXwRyb6JcjTJ5EeTFkZt
axoo5lRzGsEpZNLfUe474QKBgE5zwPNdLlTpB3wtUY8ylEI57PL2Aut7DgVrNi0a
8AE6icW1hhn0Cilva4/zINuGjfsPnPXs8ovstjBEAZ+FZwTRl0QdRtsa4niavRAX
TfMCUiYmvtQGvxS7G3Ako1Ruwm1K8ZH1hiD1CAUQ5vTkDFmERKNOa5bfNJbuNmzs
PI5/AoGAR6majJBBUDpnDkkpXu379CtweRFJMSnkxqp3rt4u05r85UUbjNulxO0b
d67z6eltOBeuPVkti8kyVzHJn4LsXyiZAj90JVN3gvN6mQHNOgxJ2dN2loORNV0C
kQJarOksOaT1MLP4aKQcCk8mvY3iLrab+MY3Fsa2P9qXuePRbMM=                                                                  
-----END RSA PRIVATE KEY-----                                                                                         
Save as [private key]: private.key
[!] File private.key exists. Overwrite? (y/n): y
[+] Saved to private.key
[+] Public Key:
 -----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAking7w3RhI8t60TL+WTu
lsDQ2VUwuiaijDn9/8nIHrX3PIOFaaYfxZFnxbR6L7bS3dJJg8txiMiffcTGgyqw
23X0haiQ1wiGPjMPxtjqsb8tZK2X8+DEXEVXP4JuLwnQ7CpHwTNOfkaOtqSocrXg
o+AGn5WBIZL6fMQyn2RY6SS5hngxDPtcyKZpIIAtgr4Lh7oLRixtEltqKO/4aggO
3BK9NOBx2SjvaJviXMcUErLME1nVmGexklsCJj+w1e3pwL8rSVfVU4KYBcgvI64U
3I52XQWA+pDwCSHG5iZ3cG5mVooSXLvLg/RslHeYw8EMVF6Z++7k+UDhvLkwUhzT
SwIDAQAB
-----END PUBLIC KEY-----
Save as [public key]: public.key
[!] File public.key exists. Overwrite? (y/n): y
[+] Saved to public.key
Press Enter to return to menu...

```

**Code Breakdown** 🧠:
- **Main Function**:
  ```python
  if __name__ == "__main__":
      rsa_main()
  ```
  - `rsa_main()` drives the CLI interface for RSA operations.

- **Key Generation**:
  ```python
  def generate_rsa_keys():
      key = RSA.generate(2048)
      private_key = key.export_key()
      public_key = key.publickey().export_key()
      print("[+] Private Key:\n", private_key.decode())
      save_to_file(private_key, priv_path, binary=True)
      print("[+] Public Key:\n", public_key.decode())
      save_to_file(public_key, pub_path, binary=True)
  ```
  - `RSA.generate(2048)` creates a 2048-bit key pair.
  - `export_key()` outputs keys.
  - Saves keys in binary mode (`wb`) to preserve formatting.

- **Saving Files**:
  ```python
  def save_to_file(data, path, binary=False):
      mode = "wb" if binary else "w"
      if os.path.exists(path):
          confirm = input(f"[!] File {path} exists. Overwrite? (y/n): ")
          if confirm.lower() != 'y':
              print("[-] Operation cancelled.")
              return False
      with open(path, mode) as f:
          f.write(data)
      print(f"[+] Saved to {path}")
      return True
  ```
  - Handles file saving with overwrite protection.


#### 2. Create a Short Message
RSA can only encrypt small data, so we use a short message.

**Command**:
```bash
echo "hi adam syed nak kopi" > syed_message.txt
```

**Example**:
```bash
┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ echo "hi adam syed nak kopi"> syed_message.txt

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat syed_message.txt 
hi adam syed nak kopi

```

#### 3. Encrypt with Public Key
Encrypt the message using the public key.

**Steps in closeSSL**:
- Select **2. RSA Encryption**, then **1. Encryption**.
- Enter `public.key` as the public key file.
- Enter `syed_message.txt` as the input file.
- Save output as `syed_message.enc`.

**Code Breakdown** 🧠:
- **Encryption Logic**:
  ```python
  def encrypt_file_rsa(pub_key_path, in_path, out_path):
      with open(pub_key_path, "rb") as f:
          pub_key = RSA.import_key(f.read())
      cipher = PKCS1_OAEP.new(pub_key)
      with open(in_path, "rb") as f:
          plaintext = f.read()
      ciphertext = cipher.encrypt(plaintext)
      save_to_file(ciphertext, out_path, binary=True)
  ```
  - `RSA.import_key` loads the public key.
  - `PKCS1_OAEP.new` uses secure OAEP padding for encryption.
  - Encrypts and saves the ciphertext in binary mode.

**Example Output**:
```

██████╗ ███████╗ █████╗       ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔══██╗      ██╔════╝████╗  ██║██╔════╝                              
██████╔╝███████╗███████║█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██╗╚════██║██╔══██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████║██║  ██║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
==================== [Disclaimer: This tools for RSA 2048 bits] ======================


1. Encryption
2. Decryption
3. Generate RSA Keys
q. Exit
Select option: 1
Enter public key file path: public.key
Enter file path to encrypt: syed_message.txt
Save as: syed_message_enc
[+] Saved to syed_message_enc
Press Enter to return to menu...


```

#### 4. Decrypt with Private Key
Decrypt the file to recover the message.

**Steps in closeSSL**:
- Select **2. RSA Encryption**, then **2. Decryption**.
- Enter `private.key` as the private key file.
- Enter `syed_message.enc` as the input file.
- Save output as `syed_message.dec`.

**Code Breakdown** 🧠:
- **Decryption Logic**:
  ```python
  def decrypt_file_rsa(priv_key_path, in_path, out_path):
      with open(priv_key_path, "rb") as f:
          priv_key = RSA.import_key(f.read())
      cipher = PKCS1_OAEP.new(priv_key)
      with open(in_path, "rb") as f:
          ciphertext = f.read()
      plaintext = cipher.decrypt(ciphertext)
      save_to_file(plaintext, out_path, binary=True)
  ```
  - Loads the private key and decrypts using PKCS1-OAEP.

**Example Output**:
```

██████╗ ███████╗ █████╗       ███████╗███╗   ██╗ ██████╗                              
██╔══██╗██╔════╝██╔══██╗      ██╔════╝████╗  ██║██╔════╝                              
██████╔╝███████╗███████║█████╗█████╗  ██╔██╗ ██║██║                                   
██╔══██╗╚════██║██╔══██║╚════╝██╔══╝  ██║╚██╗██║██║                                   
██║  ██║███████║██║  ██║      ███████╗██║ ╚████║╚██████╗                              
╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝      ╚══════╝╚═╝  ╚═══╝ ╚═════╝                              
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
==================== [Disclaimer: This tools for RSA 2048 bits] ======================


1. Encryption
2. Decryption
3. Generate RSA Keys
q. Exit
Select option: 2
Enter private key file path: private.key
Enter file path to decrypt: syed_message_enc
Save as: syed_message.dec
[+] Saved to syed_message.dec
Press Enter to return to menu...


```

#### 5. Verify the Decrypted Message
Check if the decrypted file matches the original.

**Command**:
```bash
cat syed_message.dec
diff syed_message.txt syed_message.dec
```

**Example**:
```bash
┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat syed_message.dec 
hi adam syed nak kopi

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ diff syed_message.txt syed_message.dec 

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ 


```

*No `diff` output = success! 🙌*


### Analysis 🧠
- **Security**: RSA with PKCS1-OAEP is secure but limited to small data.
- **Real-World Use**: Used in TLS key exchange and SSH authentication.

---

## **Task 3: Hashing with SHA-256** 🧮

**Objective**: Generate SHA-256 hashes for files and verify integrity by comparing hashes.

### Steps 🚶‍♂️

#### 1. Create Sample Files
Create two files, one original and one modified.

**Command**:
```bash
echo "ini last sem" > sem5.txt
echo "ini last sem saya" > sem5_modified.txt
```

**Example**:
```bash
┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ echo "ini last sem" > sem5.txt

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ echo "ini last sem saya" > sem5_modified.txt

```

#### 2. Generate Hashes
Use `closeSSL` to hash both files.

**Command**:
```bash
python main.py
```

**Steps in closeSSL**:
- Choose **1.  Hashing**.
- Enter `sem5.txt` and `sem5_modified.txt` as file paths (press Enter twice to finish).
- View the tabulated hash results.

**Example Output** (from `sha_hashing.py`):
```bash
███████╗██╗  ██╗ █████╗       ██████╗ ███████╗ ██████╗                                
██╔════╝██║  ██║██╔══██╗      ╚════██╗██╔════╝██╔════╝                                
███████╗███████║███████║█████╗ █████╔╝███████╗███████╗                                
╚════██║██╔══██║██╔══██║╚════╝██╔═══╝ ╚════██║██╔═══██╗                               
███████║██║  ██║██║  ██║      ███████╗███████║╚██████╔╝                               
╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝      ╚══════╝╚══════╝ ╚═════╝                                
                                                                                      
██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗     
██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║     
██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║     
██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║     
██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗
╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝
                                                                                      
================ [Disclaimer: This tools for Hashing using SHA-256] ==================
1. Hashing
q. Exit
Select option: 1
[*] Enter file paths one by one. Press Enter without input to finish.
File path: sem5.txt
File path: sem5_modified.txt
File path:

SHA-256 Hash Results:
+-------------------+------------------------------------------------------------------+
| Filename          | SHA-256 Hash                                                     |
+===================+==================================================================+
| sem5.txt          | 5595f76e09890e495c7253f2dde997e3f816a64c5160f35a3261428fc3340a60 |
+-------------------+------------------------------------------------------------------+
| sem5_modified.txt | 67b2527904943647f2ec0eb284c8c47fae20564b5234610e262f2e2051d9ed07 |
+-------------------+------------------------------------------------------------------+

Press Enter to return to menu...


```

#### 3. Compare Hashes
Notice the hashes are different due to the small change (without "saya" vs. with "saya" ).


### Analysis 🧠
- **How It Works**: `sha_hashing.py` uses `hashlib` to compute SHA-256 hashes in chunks for efficiency.
- **Security**: Collision-resistant, ensuring integrity.
- **Real-World Use**: SHA-256 secures Git commits and blockchain.

---

## **Task 4: Digital Signatures with RSA** ✍️

**Objective**: Sign a file with an RSA private key and verify it with the public key.

**Full Source Code**: 📄 [digital_signature.py](modules/digital_signature.py)

### Steps 🚶‍♂️

#### 1. Create a File to Sign
Create a file to sign.

**Command**:
```bash
echo "tanak kopi nak teh" > test.txt
```

**Example**:
```bash
┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ echo "tanak kopi nak teh " > test.txt

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat test.txt 
tanak kopi nak teh 


```

#### 2. Sign the File
Use the private key from Task 2 to sign the file.

**Command**:
```bash
python main.py
```

**Steps in closeSSL**:
- Select **4. Digital Signature**, then **1. Sign**.
- Enter `private.key` as the private key file.
- Enter `test.txt` as the file to sign.
- Save signature as `test.sign`.

**Code Breakdown** 🧠:
- **Main Function**:
  ```python
  if __name__ == "__main__":
      ds_main()
  ```
  - `ds_main()` runs the CLI interface for signing and verification.

- **Key Loading**:
  ```python
  def load_private_key(path):
      with open(path, "rb") as key_file:
          return serialization.load_pem_private_key(key_file.read(), password=None)

  def load_public_key(path):
      with open(path, "rb") as key_file:
          return serialization.load_pem_public_key(key_file.read())
  ```
  - Loads PEM-formatted private and public keys using `cryptography`.

- **Signing Logic**:
  ```python
  def sign_file(private_key_path, file_path, output_path):
      try:
          private_key = load_private_key(private_key_path)
          with open(file_path, "rb") as f:
              data = f.read()
          signature = private_key.sign(
              data,
              padding.PSS(
                  mgf=padding.MGF1(hashes.SHA256()),
                  salt_length=padding.PSS.MAX_LENGTH
              ),
              hashes.SHA256()
          )
          with open(output_path, "wb") as sig_file:
              sig_file.write(signature)
          print("[+] File signed successfully.")
      except Exception as e:
          print(f"[!] Error signing file: {e}")
  ```
  - Signs the file’s data using RSA-PSS with SHA-256 hashing.
  - Saves the signature in binary mode.

**Example Output**:
```bash
██████╗ ██╗ ██████╗ ██╗████████╗ █████╗ ██╗         ███████╗██╗ ██████╗ ███╗   ██╗ █████╗ ████████╗██╗   ██╗██████╗ ███████╗
██╔══██╗██║██╔════╝ ██║╚══██╔══╝██╔══██╗██║         ██╔════╝██║██╔════╝ ████╗  ██║██╔══██╗╚══██╔══╝██║   ██║██╔══██╗██╔════╝
██║  ██║██║██║  ███╗██║   ██║   ███████║██║         ███████╗██║██║  ███╗██╔██╗ ██║███████║   ██║   ██║   ██║██████╔╝█████╗  
██║  ██║██║██║   ██║██║   ██║   ██╔══██║██║         ╚════██║██║██║   ██║██║╚██╗██║██╔══██║   ██║   ██║   ██║██╔══██╗██╔══╝  
██████╔╝██║╚██████╔╝██║   ██║   ██║  ██║███████╗    ███████║██║╚██████╔╝██║ ╚████║██║  ██║   ██║   ╚██████╔╝██║  ██║███████╗
╚═════╝ ╚═╝ ╚═════╝ ╚═╝   ╚═╝   ╚═╝  ╚═╝╚══════╝    ╚══════╝╚═╝ ╚═════╝ ╚═╝  ╚═══╝╚═╝  ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝╚══════╝
                                                                                                                            
          ██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗                                 
          ██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║                                 
█████╗    ██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║                                 
╚════╝    ██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║                                 
          ██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗                            
          ╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝                            

========================= [Disclaimer: you need to generate rsa keys first if you dont have one] ===========================                                                                              
Enter key file path (private key): private.key
Enter file path to sign: test.txt
Save as (signed): test.sign
[+] File signed successfully.
Press Enter to return to menu...


```

#### 3. Verify the Signature
Verify the signature with the public key.

**Steps in closeSSL**:
- Select **4. Digital Signature**, then **2. Verify**.
- Enter `public.key` as the public key file.
- Enter `test.txt` as the file to verify.
- Enter `test.sign` as the signature file.

**Code Breakdown** 🧠:
- **Verification Logic**:
  ```python
  def verify_signature(public_key_path, file_path, signature_path):
      try:
          public_key = load_public_key(public_key_path)
          with open(file_path, "rb") as f:
              data = f.read()
          with open(signature_path, "rb") as s:
              signature = s.read()
          public_key.verify(
              signature,
              data,
              padding.PSS(
                  mgf=padding.MGF1(hashes.SHA256()),
                  salt_length=padding.PSS.MAX_LENGTH
              ),
              hashes.SHA256()
          )
          print("[✓] Signature is valid.")
      except InvalidSignature:
          print("[✗] Signature is invalid.")
      except Exception as e:
          print(f"[!] Error verifying signature: {e}")
  ```
  - Verifies the signature using the public key and RSA-PSS.
  - Raises `InvalidSignature` if the file was tampered with.

**Example Output**:
```bash
██████╗ ██╗ ██████╗ ██╗████████╗ █████╗ ██╗         ███████╗██╗ ██████╗ ███╗   ██╗ █████╗ ████████╗██╗   ██╗██████╗ ███████╗
██╔══██╗██║██╔════╝ ██║╚══██╔══╝██╔══██╗██║         ██╔════╝██║██╔════╝ ████╗  ██║██╔══██╗╚══██╔══╝██║   ██║██╔══██╗██╔════╝
██║  ██║██║██║  ███╗██║   ██║   ███████║██║         ███████╗██║██║  ███╗██╔██╗ ██║███████║   ██║   ██║   ██║██████╔╝█████╗  
██║  ██║██║██║   ██║██║   ██║   ██╔══██║██║         ╚════██║██║██║   ██║██║╚██╗██║██╔══██║   ██║   ██║   ██║██╔══██╗██╔══╝  
██████╔╝██║╚██████╔╝██║   ██║   ██║  ██║███████╗    ███████║██║╚██████╔╝██║ ╚████║██║  ██║   ██║   ╚██████╔╝██║  ██║███████╗
╚═════╝ ╚═╝ ╚═════╝ ╚═╝   ╚═╝   ╚═╝  ╚═╝╚══════╝    ╚══════╝╚═╝ ╚═════╝ ╚═╝  ╚═══╝╚═╝  ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝╚══════╝
                                                                                                                            
          ██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗                                 
          ██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║                                 
█████╗    ██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║                                 
╚════╝    ██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║                                 
          ██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗                            
          ╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝                            

========================= [Disclaimer: you need to generate rsa keys first if you dont have one] ===========================                                                                              
Enter key file path (public): public.key
Enter file path to verify: test.txt
Enter signature file path: test.sign
[✓] Signature is valid.
Press Enter to return to menu...

```

#### 4. Tamper with the File
Modify the file to test verification failure.

**Command**:
```bash
echo "Late payment incurs 5% interest" >> agreement.txt
```

**Example**:
```bash
┌┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ echo "tanak air" >> test.txt

┌──(cryptovenv)(syed㉿NWS23010037)-[~/Downloads/src/closeSSL/modules]
└─$ cat test.txt 
tanak kopi nak teh 
tanak air


```

#### 5. Verify Again
Re-run verification on the tampered file.

**Steps in closeSSL**:
- Repeat the verification steps.

**Example Output**:
```
██████╗ ██╗ ██████╗ ██╗████████╗ █████╗ ██╗         ███████╗██╗ ██████╗ ███╗   ██╗ █████╗ ████████╗██╗   ██╗██████╗ ███████╗
██╔══██╗██║██╔════╝ ██║╚══██╔══╝██╔══██╗██║         ██╔════╝██║██╔════╝ ████╗  ██║██╔══██╗╚══██╔══╝██║   ██║██╔══██╗██╔════╝
██║  ██║██║██║  ███╗██║   ██║   ███████║██║         ███████╗██║██║  ███╗██╔██╗ ██║███████║   ██║   ██║   ██║██████╔╝█████╗  
██║  ██║██║██║   ██║██║   ██║   ██╔══██║██║         ╚════██║██║██║   ██║██║╚██╗██║██╔══██║   ██║   ██║   ██║██╔══██╗██╔══╝  
██████╔╝██║╚██████╔╝██║   ██║   ██║  ██║███████╗    ███████║██║╚██████╔╝██║ ╚████║██║  ██║   ██║   ╚██████╔╝██║  ██║███████╗
╚═════╝ ╚═╝ ╚═════╝ ╚═╝   ╚═╝   ╚═╝  ╚═╝╚══════╝    ╚══════╝╚═╝ ╚═════╝ ╚═╝  ╚═══╝╚═╝  ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝╚══════╝
                                                                                                                            
          ██████╗ ██╗   ██╗     ██████╗██╗      ██████╗ ███████╗███████╗███████╗███████╗██╗                                 
          ██╔══██╗╚██╗ ██╔╝    ██╔════╝██║     ██╔═══██╗██╔════╝██╔════╝██╔════╝██╔════╝██║                                 
█████╗    ██████╔╝ ╚████╔╝     ██║     ██║     ██║   ██║███████╗█████╗  ███████╗███████╗██║                                 
╚════╝    ██╔══██╗  ╚██╔╝      ██║     ██║     ██║   ██║╚════██║██╔══╝  ╚════██║╚════██║██║                                 
          ██████╔╝   ██║       ╚██████╗███████╗╚██████╔╝███████║███████╗███████║███████║███████╗                            
          ╚═════╝    ╚═╝        ╚═════╝╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚══════╝╚══════╝╚══════╝                            

========================= [Disclaimer: you need to generate rsa keys first if you dont have one] ===========================                                                                              
Enter key file path (public): public.key
Enter file path to verify: test.txt
Enter signature file path: test.sign
[✗] Signature is invalid.
Press Enter to return to menu...


```


### Analysis 🧠
- **Security**: RSA-PSS with SHA-256 ensures authenticity and non-repudiation.
- **Real-World Use**: Used in software signing (e.g., apt) and email security (e.g., PGP).

---


---

## Problems Encountered ⚠️

- **File Overwrites**: The `save_to_file` function prevents accidental overwrites, but mistyping paths could cause issues. Always verify paths! 😅
- **RSA Size Limits**: RSA failed for large files due to key size constraints. Kept messages short to avoid errors.
- **Dependency Issues**: Missing `pycryptodome` or `cryptography` caused crashes. Fixed with `pip install`.

---

## Real-World Applications 🌍

- **AES**: Secures HTTPS, VPNs, and disk encryption (e.g., BitLocker).
- **RSA**: Powers TLS handshakes and SSH logins.
- **SHA-256**: Verifies software downloads and blockchain transactions.
- **Digital Signatures**: Authenticates software (e.g., Microsoft Store apps) and emails.

---

## Conclusion 🔚

Lab 4 was a crypto adventure! We built `closeSSL`, a Python toolkit that nails AES, RSA, SHA-256, and digital signatures. The detailed code breakdowns and interactive CLI made it a joy to develop. Ready to flex our skills in the demo! 😎

**Screenshots** 📸:
- [AES Encryption Output](./evidence/aes_encryption_output.png)
- [RSA Encryption Output](./evidence/rsa_encryption_output.png)
- [Hashing Output](./evidence/hashing_output.png)
- [Digital Signature Output](./evidence/digital_signature_output.png)