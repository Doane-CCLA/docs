# Globus Command Line Interface (CLI)

If you wish to utilize the Globus transfer tools from the command line, you can download the Globus Command Line Interface (CLI). It is available as a Python package.

## Installing the Required Tools

Since the tool is a Python package, you will need Python installed, as well as the pip installer.
* Ubuntu:   
```
sudo apt-get install python   
sudo apt-get install python-pip
export PATH="~/.local/bin:$PATH"
echo 'export PATH="~/.local/bin:$PATH"' >> "$HOME/.bashrc"
```   
* CentOS:
```
sudo yum install python   
sudo yum install python-pip
export PATH="~/.local/bin:$PATH"
echo 'export PATH="~/.local/bin:$PATH"' >> "$HOME/.bashrc"   
```
* macOS:
```
sudo easy_install python   
sudo easy_install pip
export PATH="~/.local/bin:$PATH"
echo 'export PATH="~/.local/bin:$PATH"' >> "$HOME/.bashrc"
```   
Some versions of Python will not be installed in `~/.local`. If you have trouble getting `globus` commands to execute, try the following commands to change the path:   
```
GLOBUS_CLI_INSTALL_DIR="$(python -c 'import site; print(site.USER_BASE)')/bin"   
echo "GLOBUS_CLI_INSTALL_DIR=$GLOBUS_CLI_INSTALL_DIR"   
```
```
export PATH="$GLOBUS_CLI_INSTALL_DIR:$PATH"   
echo 'export PATH="'"$GLOBUS_CLI_INSTALL_DIR"':$PATH"' >> "$HOME/.bashrc"   
```
* Windows:
    * The Windows package manager "Chocolatey" is recommended for installation. See [here](https://chocolatey.org/install) for Chocolatey installation instructions.
    * To install Python and `pip`, see [here](http://docs.python-guide.org/en/latest/starting/install3/win/#install3-windows).

* All Operating Systems:   
To install the Globus CLI, use the following command: `pip install --upgrade --user globus-cli`.

*Optional: if you wish to use the Globus CLI from within a python virtual environment, see [instructions here](https://docs.globus.org/cli/installation/virtualenv/). Otherwise, you may continue using this guide.*

To start, you will need to log in to Globus: `globus login`. Follow the instructions to get logged in. A browser window may appear.

To make sure that your login was successful, type `globus get-identities 'go@globusid.org'`. A successful output will look something like this: `c698d42e-d274-11e5-bf75-1fc5bf53bb56`.

## Globus CLI Basics

* Endpoint Search
    ```
    $ globus endpoint search 'CCLA HPC'
    ID                                   | Owner                 | Display Name  
    ------------------------------------ | --------------------- | --------------
    57230a10-7ba2-77e7-8c3b-22555b9923ef | cclahpc@globusid.org     | CCLAHPC      
    ```
* Endpoint Management
    * _Use variables for endpoint IDs:_ Endpoint IDs are cumbersome. You cannot rename them, but you can store them as variables. For example:
        ```
        epCCLAHPC=57230a10-7ba2-77e7-8c3b-22555b9923ef
        ```
        Now you can use the variable to display information and manage files (with truncated output):
        ```
        $ globus endpoint show $epCCLA-HPC
        Display Name:              CCLA-HPC
        ID:                        57230a10-7ba2-77e7-8c3b-225550b9923ef
        Owner:                     ccla@globusid.org
        Activated:                 True
        Shareable:                 True
        Department:                CCLA
        Organization:              Doane Univ
        Department:                CCLA
        Visibility:                True
        Default Directory:         /~/
        Force Encryption:          False
        Managed Endpoint:          True
        ```
    * _Make a directory:_
        ```
        globus mkdir $epCCLAHPC:~/example_dir
        ```
    * _List the contents of a directory:_
        ```
        $ globus ls $epCCLAHPC:~/
        example_dir/
        ccla-user-guide.pdf
        hello-world.c
        hello-world.pbs
        ```
    * _File transfer between endpoints:_
        * First, search for a second endpoint. Then set that endpoint as a Bash variable.
            ```
            $ globus endpoint search 'Globus Tutorial Endpoint' \
                  --filter-owner-id 'c699d42e-d274-11e5-bf75-1fc5bf53bb24'
              Owner           | ID                                   | Display Name
              --------------- | ------------------------------------ | ---------------------------
              go@globusid.org | ddb59aef-6d04-11e5-ba46-22000b92c6ec | Globus Tutorial Endpoint 1
              go@globusid.org | ddb59af0-6d04-11e5-ba46-22000b92c6ec | Globus Tutorial Endpoint 2
              go@globusid.org | cf9bcaa5-6d04-11e5-ba46-22000b92c6ec | Globus S3 Tutorial Endpoint
            $ epGLOBUS1=ddb59aef-6d04-11e5-ba46-22000b92c6ec
            ```
        * Make a single file transfer from epCCLAHPC to epGLOBUS1.
            ```
            globus transfer $epCCLAHPC:/ccla-user-guide.pdf $epGLOBUS:~/ccla-user-guide.pdf \
            --label "user-guide"
            ```
        * Make a batch transfer.
            ```
            $ globus transfer $epCCLAHPC:/example_dir/ $epGLOBUS:~/ \
            --batch --label "CCLA Batch" < in.txt
            ```

## Related Tutorials
* [Globus Endpoints](globus-endpoints.md)
* [Graphical SFTP](graphical-sftp.md)
