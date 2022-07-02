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

## If you want to know more about github Encrypted-secrets then click on below Link:
 https://docs.github.com/en/actions/security-guides/encrypted-secrets 

### GITHUB Functions & Expression ###
- You can use expressions to programmatically set environment variables in workflow files and access contexts. An expression can be any combination of literal values, references to a context, or functions
- You can Define expression at job level & steps level also.
- Github Expression can be anything  related to contexts.


## EXAMPLE EXPRESSION WITH IF STATEMENT: ##
    if: ${{ expression }}
    if: ${{ github.event_name == 'push' }}
    if: ${{ always() }}

## For more examples about expression & context Link on below link: ##
https://docs.github.com/en/actions/learn-github-actions/contexts


#### GITHUB ACTIONS ERROR HANDLING & Timeout ###
- You can also handles errors in github actions as we are doing in jenkins or jenkins.
- If you think their is any steps in a github workflow that can produce error and will result in failure of  workflow then you can use it.
- Timeout function in github workflow is very useful when you know that your workflow or action will take longer time then expected. Then you can define a timeout inside your job. 
- Default timeout time in github action is 1-2 minutes

## ERROR HANDLING EXAMPLE: ##
    jobs:
    run-github-actions:
        runs-on: ubuntu-latest
        steps:
        - name: Error step
            run: eccho "This Will not run"
            continue-on-error: true
        - name: Testing steps
            run: echo "steps to run after error step"

## TIMEOUT HANDLING EXAMPLE:  ##

    jobs:
    run-github-actions:
        runs-on: ubuntu-latest
        steps:
        - name: Error step
            run: echo "This Will take longer time execute"
            timeout-minutes: 2

### MATRIX & STRATERGY CONTEXT IN GITHUB ACTION ###
- The matrix context contains the matrix properties defined in the workflow file that apply to the current job.
- The strategy context contains information about the matrix execution strategy for the current job

## EXAMPLE FOR MATRIX: ##

    jobs:
      node0-version-changes:
        strategy:
          matrix:
           os: [macos-latest,ubuntu-latest,windows-latest]
           node_version: [6,8,10,14]
          fail-fast: true
          max-parallel: 2
        runs-on: ${{matrix.os}}
        steps: 
        - name: node version
            run: node -v
        - name: changing node version
            uses: actions/setup-node@v3
            with:
            node-version: ${{ matrix.node_version }}


### SNYK Vulnerabilities Scanner ###
- Synk is Saas tool which is used to find the vulnerabilities inside the Code. It is available in Github Marketplace.
- To configure Snyk with Github Action. Firstly you need create a account in 
    snyk.io
- After account is created you need to copy the token the snyk account and save as secret in github account.
- Snyk is used to find the vulnerabilities in open source and thirdy party library, IAC & in containers.
- Snyk is available as SaaS.
- It is also called as SAST.(Static  Application  Security Testing).

## Example: ##
        name: Example workflow for Node using Snyk
        on: push
        jobs:
        security:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@master
            - name: Run Snyk to check for vulnerabilities
                uses: snyk/actions/node@master
                continue-on-error: true
                env:
                SNYK_TOKEN: ${{ secrets.SNYK_SECRET }}

### For more Click on Below link: ###:
    https://github.com/marketplace/actions/snyk