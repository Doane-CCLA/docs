# Globus Endpoints

Globus Endpoints are storage systems to which you have access. Once an Endpoint is located or created Globus saves the location for you so you do not need to repeatedly search type paths.

Endpoint Search Term(s) | Storage System | Path              | Description
----------------------- | -------------- | ----------------- | ---------------------------------------------------------
CCLA HPC                | NFS            | /~/               | User home directory
CCLA HPC                | NFS            | /data/            | NFS project directories
CCLA HPC                | Lustre         | /lustre/tigris/   | Project directories. High-performance, temporary storage.



&#128221; **Note:** If you're having trouble finding an existing Endpoint, [contact the CCLA team](../SUPPORT.md).

## Setting Up Endpoints   

1. Click in the Endpoint box on the left side and search for `CCLA HPC`.
-  You will be redirected to enter your credentials.
    * Authenticating the Endpoint with your credentials is known as *Endpoint Activation* and can be done when adding and using an Endpoint for the first time, or can be completed by navigating to the "Manage Endpoints" screen (`Endpoints`&rarr;`Endpoint List`&rarr;`activate`).    
-  Once the endpoint is set you can modify the path to point to your file/data. In this example, we will connect to Lustre storage: `lustre/tigris/ccla/proj-shared`
-  On the right side, set the endpoint. We will use a Globus Tutorial endpoint. Search for `Globus Tutorial Endpoint`.
-  Again, you may adjust the path. Your home directory is default.

## Creating an Endpoint on your Personal or Work Computer
It is easy to use your personal or work computer as a Globus Endpoint. Follow the instructions below.

&#128221; **Note:** You may need to create a firewall exception for the Globus Personal Client. For configuration instructions, please consult the [details](https://docs.globus.org/how-to/configure-firewall-gcp/) on the Globus site.

1. Choose a descriptive name for your endpoint and click `Generate Setup Key`.
- Copy the Setup Key. You will paste this into the software during setup.
- Navigate to the [Globus Personal Connect webpage](https://www.globus.org/globus-connect-personal) to download the client onto your personal computer.
-  Click on the name of your operating system to obtain detailed instructions for installing the client and setting up the Endpoint.   
- Once the client is installed, launch the program. You will be prompted to paste your setup key.
    &#128221; **Note:** The Globus Personal Endpoint Client may produce errors if you are connected via VPN.
- Now you may use the Globus web interface or the [command line interface](globus-command-line-interface.md) to search for your new endpoint using the name you provided in step 1.
