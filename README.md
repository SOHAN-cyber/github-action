===========================================
Github Workflow for encyption & decryption
******************************************
GPG(GNU Privacy Guard)

 GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications
It is also pre installed in Ubuntu OS.You only need to run the command to encrypt it

***********************
    GPG COMMAND:
                        gpg --symmetric --cipher-algo AES256 secret 
**************************
Now you have another file named as secret.gpg which wll be encrypted file and that can be decrypted using password that you provides
                cat secret.json
