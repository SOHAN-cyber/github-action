# ***GITHUB  WORKFLOW FOR ENCRYPTION & DECRYPTION A FILE IN GITHUB RUNNER***

## GPG(GNU Privacy Guard)

 GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications
It is also pre installed in Ubuntu OS.You only need to run the command to encrypt it

***********************
## **GPG COMMAND FOR ENCRYPTING FILE CONTENT:**
                        gpg --symmetric --cipher-algo AES256 secret 

In If you want to decrypt the file in Github Runner then you need to pass the password as secret in github runner and for the you need to make use of
- Github Secrets
- Github Workflow enviornmental variable in which you will pass th value of Github Secret
##  **GPG COMMAND FOR DECRYPTING FILE CONTENT:**
                gpg --quiet --batch  --yes --decrypt --passphrase="$PASS"  --output $HOME/secret.json secret.gpg


