## Task 
We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.

On storage server in Stratos Datacenter we have private and public keys stored at /home/*_key.asc. Use these keys to perform the following actions.

- Encrypt /home/encrypt_me.txt to /home/encrypted_me.asc.

- Decrypt /home/decrypt_me.asc to /home/decrypted_me.txt. (Passphrase for decryption and encryption is kodekloud).

- The user ID you can use is kodekloud@kodekloud.com.
## Solution 

Connect to the storage server.
```sh
thor@jump_host ~$ ssh ststor01@natasha
```

Change directory to `/home/`.
```sh
[natasha@ststor01 ~]$ cd ..
[natasha@ststor01 home]$ ls
ansible         encrypt_me.txt  private_key.asc
decrypt_me.asc  natasha         public_key.asc
```

Import public_key.asc.
```sh
[natasha@ststor01 home]$ sudo gpg --import public_key.asc
```

Encrypt the file.

```sh
sudo gpg --encrypt --recipient kodekloud@kodekloud.com --output encrypted_me.asc encrypt_me.txt 
```

Decrypt the file. When prompted to enter passphrase enter `kodekloud`.
```sh
[natasha@ststor01 home]$ sudo gpg -d -o decrypted_me.txt decrypt_me.asc
```

## References

[How to Encrypt and Decrypt Files Using GPG in Linux](https://www.tecmint.com/gpg-encrypt-decrypt-files/)
