The testing of running the application factory application in a Windows environment was done using Windows 10 running
in a VirtualBox virtual machine.  The user involved had administration access.  The exercise was done to identify any
application issues when running in Windows as a precursor to running the application using IIS.  

The setup of a Windows 10 machine consisted of four configuration areas:

1. VirtualBox virtual machine 
2. Services REST API  
  2a. Postgresql Database
3. Vue Web Application

# VirtualBox Virtual Machine
The Windows 10 appliance was setup using an existing Windows 10 VM and the steps to create a Windows VM will not be 
covered here.

### Networking
Two way access is necessary between the Host machine and the guest (Windows) machine so that the browser can be run in 
the host machine accessing the Vue and Services applications on the guest machine while also allowing the guest
machine's service application to access a Postgres database running on the host.  Doing this simulated the Postgres
database running on a separate server and allowed the re-use of application data without the need to configure another
Postgres database.

The two way communication was setup by defining the VM's network with the host machine.  The VM was connected to a 
host-only network adpator for communication between the host and guest machines and a NAT adaptor for Internet access. 
#### Host-only Network
>Host-only Networking Description  
>
>With host-only networking, virtual box doesn't try to use a physical network adapter on the host. Instead in VirtualBox 
you can create one or more (up to 8) virtual adapters for connections between the host and virtual machines created in 
VirtualBox on the host.
>
>A VirtualBox host-only adapter can also function as a DHCP server to assign ip addresses to VirtualBox virtual machines.
The host machine (and other virtual machines if any) can then connect to the virtual machines using these ip addresses 
using ssh or sftp (provided an ssh server is running on the virtual machine).


The host-only network was created when the Windows VM was created, but can be checked by selection File/Host Network 
Manager from the VirtualBox toolbar.  The 'vboxnet0' adaptor was set to the following:
[[/images/environment-configs/virtualbox/host-only network.png|Host-only Network]]
#### Windows virtual machine
Two 'Adaptors' are configured on the guest machine using the Settings dialog and going to the Network tab.   
__Host-only Adapter Configuration__   
[[/images/environment-configs/virtualbox/guest-adapter1.png|Guest Adaptor 1]]   
__Internet Configuration__   
[[/images/environment-configs/virtualbox/guest-adapter2.png|Guest Adaptor 2]]

##### Software Installations
Once the virtual machine can connect to the Internet it is possible to install Node, Git, and Webstorm (IDE) on the 
virtual machine.

* Install NPM/Node from https://nodejs.org/en/download/ (.msi)
* Install Git by downloading from https://git-scm.com/downloads and running the installation.  
* Install an IDE (Webstorm in this example)

##### Shared Folders
Disk shares are set to allow access of data on the host from the guest.  These can be used to access downloads and 
provide areas where data can be stored on the host.  However, the 'volumes' share is critical in providing a place to
store attachments and query results which will be accessed using the __APPFACTORY_VOLUME_PATH__ environment variable.  
__Shared Folders__  
[[/images/environment-configs/virtualbox/shared folders.png|Shared Host Folders]]   


# Services REST API
* Clone services repo and run npm install
``` javascript 
mkdir \workspace  
cd \workspace
git clone https://github.com/gmarshall142/appfactory-services.git
rd appfactory-services services
cd services
npm install
npm run build
```
* Set git global attributes 
``` javascript
git config --global user.email "gmarshall142@gmail.com"
git config --global user.name "gmarshall142" 
git config --global user.password "*******"
```

* Setup a debug configuration that will run the services application (Webstorm example)
This configuration will run the services application in debug mode.  Prior to starting the service the project build 
script is run.  
__Services Debug Config__    
[[/images/environment-configs/virtualbox/services debug config.png|Services Debug Configuration]]
__Services Debug Config Build Step__     
[[/images/environment-configs/virtualbox/services debug config build step.png|Services Debug Configuration Build Step]]   

* Obtain the IP addresses for both the host and guest machines
__Host IP__  
``` javascript
~ $ ifconfig | grep 192.168
	inet 192.168.1.4 netmask 0xffffff00 broadcast 192.168.1.255
	inet 192.168.56.1 netmask 0xffffff00 broadcast 192.168.56.255
```                    
__Guest IP__  

``` javascript
C:\Users\gmarshall>ipconfig

Windows IP Configuration


Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::cc77:2181:e856:4438%3
   IPv4 Address. . . . . . . . . . . : 192.168.56.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . : home
   Link-local IPv6 Address . . . . . : fe80::59a0:e201:c7f5:60cf%9
   IPv4 Address. . . . . . . . . . . : 10.0.3.15
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 10.0.3.2ipconfig
```                    
* Environment Variables
Environment variables are used to set values in the application such as user, password, host, port, etc.  The following 
environment variables are set in the GUEST machine:
* NODE_ENV=development    
* POSTGRES_HOST=__*host IP*__   
* POSTGRES_NAME=appfactory
* POSTGRES_PORT=5432
* POSTGRES_PSWD=__*postgresql database user password*__
* POSTGRES_USER=appuser
* VUE_APP_REST_HOST=__*guest IP*__
* VUE_APP_REST_PORT=3000
* APPFACTORY_VOLUME_PATH=w:\

#### Postgresql Database
The Postgresql database runs on the HOST and is accessed using the POSTGRES_* environment variables.  In addition to
using the environment variables to set connection variables it is also necessary to take steps on the HOST to allow the
database connection from a machine other than the HOST machine.  The access is configured by modifications to the 
following configuration files on the HOST:
* modify __postgresql.conf__ file to allow connections using IP address; add the following 'listen_addresses' line:
``` javascript
#------------------------------------------------------------------------------
# CONNECTIONS AND AUTHENTICATION
#------------------------------------------------------------------------------

# - Connection Settings -
listen_addresses = '*'
```     
* modified postgresql pg_hba.conf file to allow requests to IP address by adding a line referencing the HOST IP
``` javascript
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
host    all             all             192.168.1.4/24          trust
```

# Vue Web Application
##### Clone services repo and run npm install
``` javascript 
cd \workspace
git clone https://github.com/gmarshall142/appfactory.git
cd appfactory
npm install
```
* Install Vue CLI
``` javascript 
npm install -g @vue/cli
```
##### Environment Variables
Environment variables are used to set development variables and the application protocol to use:
* VUE_APP_EMAIL=__*default user email*__
* VUE_APP_PSWD=__*default user password*__
* VUE_APP_MODE=DEV
* VUE_APP_LEVEL=debug
* VUE_APP_PROTOCOL=http
##### Environment variables that control the sockjs callbacks from the Vue app
* VUE_APP_WEB_HOST=__*guest IP*__
* VUE_APP_WEB_PORT=8080

