[CADES](http://support.cades.ornl.gov/) &rarr; [User Documentation](../README.md) &rarr; [Globus Overview](globus-overview.md) &rarr; [Globus Command Line Interface](globus-command-line-interface.md)

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
    $ globus endpoint search 'CADES OR'
    ID                                   | Owner                 | Display Name  
    ------------------------------------ | --------------------- | --------------
    57230a10-7ba2-11e7-8c3b-22000b9923ef | cades@globusid.org    | CADES-OR      
    ```
* Endpoint Management
    * _Use variables for endpoint IDs:_ Endpoint IDs are cumbersome. You cannot rename them, but you can store them as variables. For example:
        ```
        epCADESOR=57230a10-7ba2-11e7-8c3b-22000b9923ef
        ```
        Now you can use the variable to display information and manage files (with truncated output):
        ```
        $ globus endpoint show $epCADESOR
        Display Name:              CADES-OR
        ID:                        57230a10-7ba2-11e7-8c3b-22000b9923ef
        Owner:                     cades@globusid.org
        Activated:                 True
        Shareable:                 True
        Department:                CADES
        Organization:              Oak Ridge National Lab
        Department:                CADES
        Visibility:                True
        Default Directory:         /~/
        Force Encryption:          False
        Managed Endpoint:          True
        ```
    * _Make a directory:_
        ```
        globus mkdir $epCADESOR:~/example_dir
        ```
    * _List the contents of a directory:_
        ```
        $ globus ls $epCADESOR:~/
        example_dir/
        cades-user-guide.pdf
        hello-world.c
        hello-world.pbs
        ```
    * _File transfer between endpoints:_
        * First, search for a second endpoint. Then set that endpoint as a Bash variable.
            ```
            $ globus endpoint search 'OLCF ATLAS'
            ID                                   | Owner             | Display Name
            ------------------------------------ | ----------------- | ------------
            ef1a9560-7ca1-11e5-992c-22000b96db58 | olcf@globusid.org | OLCF ATLAS  
            $ epATLAS=ef1a9560-7ca1-11e5-992c-22000b96db58
            ```
        * Make a single file transfer.
            ```
            globus transfer $epCADESOR:/cades-user-guide.pdf $epATLAS:~/cades-user-guide.pdf \
            --label "user-guide"
            ```
        * Make a batch transfer.
            ```
            $ globus transfer $epCADESOR:/example_dir/ $epATLAS:~/ \
            --batch --label "CADES Batch" < in.txt
            ```

## Related Tutorials
* [Globus Endpoints](globus-endpoints.md)
* [Graphical SFTP](graphical-sftp.md)
