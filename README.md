# Installaton on Windows

1. [Download](https://downloads.stardog.com/stardog/stardog-latest.zip) the distribution .

2. Unzip the file and open a command prompt.

3. Setup STARDOG_HOME

    ``The most important piece of configuration to complete before you start the Stardog server is setting the STARDOG_HOME environment variable. This is the directory where       all the Stardog databases and other files will be stored.``


* Create the directory to set STARDOG_HOME to in Command Prompt.
   
   `mkdir D:\Users\stardog\stardog_home`

* Set the STARDOG_HOME environment variable to the directory we just created.
   * Launch “Control Panel” > “System” > “Advanced system settings” > Switch to “Advanced” tab > “Environment variables” > Choose “New” > Enter STARDOG_HOME for the variable and provide the path to the newly created directory as the value.

4. Copy your Stardog license into the STARDOG_HOME directory:

      * If you do not have a license, you can obtain one on the [Stardog](https://www.stardog.com/get-started/) website.
      * Once you have a license, copy or move your license key to your STARDOG_HOME directory created in the previous step.

5. Place the bin folder of the unzipped Stardog distribution on your PATH so the stardog.bat and stardog-admin.bat scripts can be used regardless of current working directory.

    `Launch “Control Panel” > “System” > “Advanced system settings” > Switch to “Advanced” tab > “Environment variables” > Select the entry containing Path, Choose “Edit”`

6. Execute the provided batch script install-service.bat in the bin directory to install Stardog as a Windows service.

    ` .\install-service.bat `
    
    
    You should see output in your prompt indicating the service was successfully installed:
    
    
    ```AMD64 Architecture detected

     The following parameters will be set for the service

     Stardog installation directory is D:\Users\stardog\stardogs\stardog-7.4.0
     STARDOG_HOME is D:\Users\stardog\stardog_home
     Stardog server will use 2048 MB
     Server logs will be written to D:\Users\stardog\stardogs\stardog-7.4.0\logs

     Installing Service "Stardog Server"

     Successfully installed "Stardog Server" ```
     
7. Start the server by using below command :

    `stardog-admin server start`
    
8. Troubleshooting
    * INSUFFICIENT PERMISSIONS:
    
        **Run command Prompt as a Administrator to install stardog.**

    * UNABLE TO FIND A VALID LICENSE:

        **If you have a valid license, copy or move the license to your STARDOG_HOME directory.**
        
        **If you do not have a license, you can obtain one on the [Getting Started Page](https://www.stardog.com/get-started).**

# Installaton on Linux.

### Debian Based Systems

To install Stardog using apt-get run the following commands:

            $ curl http://packages.stardog.com/stardog.gpg.pub | apt-key add
            $ echo "deb http://packages.stardog.com/deb/ stable main" >> /etc/apt/sources.list
            $ apt-get update
            $ apt-get install -y stardog[=<version>]
      
This will first add the Stardog gpg key to the systems and then fetch and install the latest Stardog deb package.

Stardog binaries should now be in the /opt/stardog directory.

### RPM Based systems

To install Stardog using yum run the following commands:

            $ curl http://packages.stardog.com/rpms/stardog.repo > /etc/yum.repos.d/stardog.repo
            $ yum install -y stardog[-<version>]
            
 Stardog binaries should now be in the /opt/stardog directory.
 
 ### Amazon EC2
 
 Certain Amazon EC2 instances do not let you redirect output into /etc/yum.repos.d as specified above. On such instances you can install Stardog like so:
 
            $ sudo yum-config-manager --add-repo http://packages.stardog.com/rpms/stardog.repo
            $ sudo yum-config-manager --enable stardog
            $ yum install -y stardog[-<version>]
            
Stardog binaries should now be in the /opt/stardog directory.


### Package Layout

The packages require that OpenJDK 8 and all of its dependencies are installed on the system. The package managers will install them if they are not already there. Stardog is then configured to start on boot via systemd and thus it can be controlled by the systemctl tool as shown below:

            $ systemctl start stardog
            $ systemctl restart stardog
            $ systemctl stop stardog
            
##### Customize Stardog’s Environment

To customize the environment in which stardog is run the file /etc/stardog.env.sh can be altered with key value pairs, for example:

            export STARDOG_HOME=/var/opt/stardog
            
By default, the STARDOG_HOME environment variable will be set to /var/opt/stardog as seen above. This is the directory where all the Stardog databases and other files will be stored. You may change this environment variable.


# Stardog studio

**Stardog Studio is the IDE for the Knowledge Graph Engineer designed to make Stardog functionality easier to use for everyday users.**

### Steps to obtain Stardog Studio and connect to a running Stardog server:

1. Stardog Studio can be accessed in the [browser](http://stardog.studio/).
2. Start up the Studio application.
3. Select the “Connect to Stardog” button to connect to a running Stardog server.
4. Enter your credential details. Stardog starts up by default at http://localhost:5820. Stardog also comes with a default superuser **admin** with a password of **admin**. For illustrative purposes, we use this admin user here to get started but this is in general not safe and should be changed before deploying Stardog into production.


### Using Stardog Studio in the browser via Docker

If you want to run Studio in the browser yourself, it is distributed in a pre-configured Docker image via [DockerHub](https://hub.docker.com/). 

To get the latest version of in-browser Studio, perform the following steps:

1. Open a command line terminal
2. Enter the following:

            docker pull stardog/stardog-studio:current
            
3. Once the command in step 2 completes, enter :

            docker run --name=stardog-studio -p 8888:8080 -d stardog/stardog-studio:current

    * Note the first number, the one before the `:` in the `-p 8888:8080` argument, is the port Studio will run on locally. This can be any port number you choose, but note             that in later steps, we’re assuming `8888`
    * The `--name=stardog-studio` argument names the container as “stardog-studio” so that you can easily reference it later; you could choose another name here, if you’d          like.

4. When the command in step 3 completes successfully, you should see a long string ID printed out in the terminal – this is the ID of the running Docker container; you can ignore it for present purposes. You can now access Studio in your browser by going to http://localhost:8888, again, substituting whatever port number you chose.

At this point, you can stop and start the container whenever you need it, running docker stop stardog-studio and docker start stardog-studio, respectively (using whatever name you provided in step 3, above). The Docker Daemon and the Studio container must be running to access in-browser Studio. If Studio is not accessible please remember to start Docker, as it may not start automatically on startup

# Stardog admin commands

$DB will be replaced by the database name in each command

1. Database creation
        
            stardog-admin db create -o spatial.enabled=true -o search.enabled=true -n $DB
            
2. Database deletion

            stardog-admin db drop $DB
            
3. Adding Prefix to the database :

            stardog namespace add $DB --prefix "" --uri http://www.example.org/fraud_detection#

            stardog namespace add $DB --prefix wgs --uri http://www.w3.org/2003/01/geo/wgs84_pos#

4. Mapping with csv files using turtle files:

            stardog-admin virtual import $DB example.ttl example.csv
            
5. Making virtual graph using data from other sources like mysql.

            stardog-admin virtual add examples.properties examples.ttl
            
