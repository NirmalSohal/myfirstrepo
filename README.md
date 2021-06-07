# Installaton on Windows

1. [Download](https://downloads.stardog.com/stardog/stardog-latest.zip) the distribution .

2. Unzip the file and open a command prompt.

3. Setup STARDOG_HOME

    ``The most important piece of configuration to complete before you start the Stardog server is setting the STARDOG_HOME environment variable. This is the directory where       all the Stardog databases and other files will be stored. If STARDOG_HOME is not defined, Stardog will use the Java user.dir property value.``


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


