# ***GITHUB  WORKFLOW FOR ENCRYPTION & DECRYPTION A FILE IN GITHUB RUNNER***

## GPG(GNU Privacy Guard)

 GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications
It is also pre installed in Ubuntu OS.You only need to run the command to encrypt it

***********************
## **GPG COMMAND FOR ENCRYPTING FILE CONTENT:**
                        gpg --symmetric --cipher-algo AES256 secret 

If you want to decrypt the file in Github Hosted Runner then you need to pass the password as secret in github runner and for that you  need to make use of
- Github Secrets: It will be used to save the password as secret in github. Which will secure your password to be expose as plain text.
- Github Workflow: Where you will call your secret as enviornmental variable.
##  **GPG COMMAND FOR DECRYPTING FILE CONTENT:**
                gpg --quiet --batch  --yes --decrypt --passphrase="$PASS"  --output $HOME/secret.json secret.gpg


