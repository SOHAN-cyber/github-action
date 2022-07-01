# ***GITHUB  WORKFLOW FOR ENCRYPTION & DECRYPTION A FILE IN GITHUB RUNNER***

## GPG(GNU Privacy Guard)

 GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications
It is also pre installed in Ubuntu OS.You only need to run the command to encrypt it

***********************
## **GPG COMMAND FOR ENCRYPTING FILE CONTENT:**
                        gpg --symmetric --cipher-algo AES256 secret 

## *DECRYPTING FILE CONTENT AT RUNTIME IN GITHUB RUNNER*

If you want to decrypt the file in Github Hosted Runner then you need to pass the password as secret in github runner and for that you  need to make use of
- Github Secrets: It will be used to save the password as secret in github. Which will secure your password to be expose as plain text.
- Github Workflow: Where you will call your secret as enviornmental variable.

##  **GPG COMMAND FOR DECRYPTING FILE CONTENT:**
                gpg --quiet --batch  --yes --decrypt --passphrase="$PASS"  --output $HOME/secret secret.gpg

# Short Description about decryption the command
 - quiet: Try to be as quiet as possible.
 - batch: Use batch mode. Never ask, do not allow interactive commands.
 - yes: It is  for everything that gpg need to run this in as we can't enter anything at run time inside github runner.
 - decrypt: It is for decrypting the file.
 - output: It is to store decrypted file in location $HOME/secret.json.
 - secret.json: It is path of file which needs to be decrypt. This file is in pwd in our case.

### **Now if you want to view the context of file of encrypted file then run the below command:**
                                         cat $HOME/secret

## If you want to know more about github sencrypted-secrets then click on Link:
 https://docs.github.com/en/actions/security-guides/encrypted-secrets 
