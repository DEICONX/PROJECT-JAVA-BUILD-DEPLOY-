# AWS BUILD SERVER CREATION

### LAUNCH EC2

> create a instance by giving instance name 

![](BUILD%20SERVER/Screenshot%202025-10-07%20120405.png)

----

> select ubuntu image and make sure it is latest version i.e 24.04 LTS (HVM)

![](BUILD%20SERVER/Screenshot%202025-10-07%20120428.png)

----

> click on edit network settings and change security group name(optional) and launch instance

![](BUILD%20SERVER/Screenshot%202025-10-07%20120507.png)

----

> connect to the instance

![](BUILD%20SERVER/Screenshot%202025-10-07%20120622.png)

----

> copy the SSH key and open terminal 

![](BUILD%20SERVER/Screenshot%202025-10-07%20120636.png)

---

> In terminal change directory to downloads(your PEM file is present in downloads)
> use the below command:
> `cd downloads` and press enter
> paste the SSH key and press enter now it will ask permission yes/no type yes 

![](BUILD%20SERVER/Screenshot%202025-10-07%20120714.png)

-----

> Now you are connected to BUILD server image(ubuntu) 

![](BUILD%20SERVER/Screenshot%202025-10-07%20120731.png)

# JAVA BUILD-MAVEN 

#### GIT CLONE

 >Open the GITHUB repo where JAVA code is stored in browser

![](Screenshot%202025-10-07%20121029.png)

-----

>Now copy the HTTPS URL(click on code down arrow to find the URL as shown in below image)

![](Screenshot%202025-10-07%20121049.png)

-----

> Now in terminal:
> run `git clone <YOUR URL>` and your code is cloned(downloaded) in your BUILD server 
>
> use the following commands:
>
> `ls` - to view the list of folders in repo
>
> `cd <folder name>` - to change directory 

![](Screenshot%202025-10-07%20121131.png)

-----

> Again use `ls` to view the files/folders present in the code repo
> read the POM file by using `cat pom.xml` and we get to know build tool and JAVA version developer mentioned

![](Screenshot%202025-10-07%20121220.png)

------

> Now update the system and install JAVA by using 
>
> `sudo apt update -y`
>
> `sudo apt install openjdk-17-jre-headless -y` 

![](Screenshot%202025-10-07%20121307.png)

-----

> After Installing JAVA now install maven using
>
> `sudo  apt install maven -y`

![](Screenshot%202025-10-07%20121410.png)

------

> validate the CODE by using
>
> `mvn validate`

![](Screenshot%202025-10-07%20121516.png)

----

> To build the code use this command:
>
> `mvn package` 

![](Screenshot%202025-10-07%20121536.png)

-----

> You will get build failure as we have downloaded latest version of JAVA and Developer mentioned JAVA 8 version in POM file 
>
> now FIX it (in real time the DEVELOPER will fix the POM file) 

![](Screenshot%202025-10-07%20121604.png)

-----

> I have Used CHATGPT to fix the POM file
>
> Below is the updated POM file now copy the updated POM file

![](Screenshot%202025-10-07%20121856.png)

-----

>Now erase the pom.xml by using `>pom.xml` cmd
>
>Open vi editor using `vi pom.xml` and by pressing I paste the updated pom file inside it use `:wq` to save it

![](Screenshot%202025-10-07%20121929.png)

--------

> Use `mvn clean` to remove the previous failed build

![](Screenshot%202025-10-07%20122020.png)

------

> Now run `mvn package` again with new updated pom.xml 

![](Screenshot%202025-10-07%20121536.png)

---

> Build Success and code Build is completed 

![](Screenshot%202025-10-07%20122106.png)

-----

> To view the Artifact (.war) use `ls` and `cd target` ,`ls` again u can see .war file in red  

![](Screenshot%202025-10-07%20122127.png)

--------

# AWS DEPLOY SERVER CREATION AND CONFIGURATION

#### LAUNCH EC2

> create an instance by giving instance name

![](deploy%20server/Screenshot%202025-10-07%20123614.png)

-----

> select image ubuntu latest version same as BUILD server and launch the server

![](deploy%20server/Screenshot%202025-10-07%20123752.png)

-----

>  configure inbound rules
> go to security and u will find inbound and outbound rules 

![](deploy%20server/Screenshot%202025-10-07%20123812.png)

----

>  select edit inbound rules to add port number of TOMCAT WEB Server

![](deploy%20server/Screenshot%202025-10-07%20123824.png)

----

>Add port number 8080 
>
>Type: custom TCP ; Port range: 8080 ; Source: Anywhere IPV4

![](deploy%20server/Screenshot%202025-10-07%20123849.png)

-----

> After adding inbound rule click save rules and it will show successfully modified

![](deploy%20server/Screenshot%202025-10-07%20123900.png)

-----

> copy the SSH key and open Terminal

![](deploy%20server/Screenshot%202025-10-07%20123927.png)

-----

> Use `cd downloads` to get into PEM file location which is saved in downloads
>
> Now paste the SSH key and enter yes you will be connected to DEPLOY server

![](deploy%20server/Screenshot%202025-10-07%20124017.png)

----

# BUILD CODE DEPLOYMENT-TOMCAT WEB SERVER

> Update the server using `sudo apt -y update`
>
> Install JAVA latest version by using `sudo apt install openjdk-17-jre-headless -y`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125258.png)

---

> Browse apache tomcat install and open the website
>
> copy the address(URL Link) of tar.gz(pgp,sha512) file

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125403.png)

----

> Use `wget <tar.gz link address>` to download the folder

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125433.png)

----

> By using `ls` u can find downloaded folder
>
> to extract the folder use `tar -xvf apache-tomcat-9.0.110.tar.gz` 

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125500.png)

------

> Use `ls` to see the extracted folder
>
> Change directory to extracted folder `cd <folder name>` 
>
> To see the files/folders inside extracted folder use `ls`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125533.png)

------

> Now change directory to bin folder `cd bin`
>
> Start TOMCAT server using `./startup.sh`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20125927.png)

----

> To check whether the web server is started or not copy the public ip of DEPLOY server 

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20130038.png)

----

>Open New Icognito window and paste your IP along with Web server port number i.e <your IP>:8080 in the image it is 
>
>Ex: 54.91.69.103:8080

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20130105.png)

---

> Your TOMCAT Web server is started and you can see in the below image

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20130119.png)

---

> Select master option in the above image and you will be redirected to the page which shows 403 error
>
> You have to configure the WEB server 

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20130129.png)

--------

> First add a user for WEB server to do that
>
> `ls` lists all the files/folders
>
> change directory to `cd conf/`  and `ls` to see all the files/folders present inside it
>
> open file using `vi <file name>` here in the below image it is `vi tomcat-users.xml`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20134932.png)

-----

> Add User at bottom above </tomcat-users>
>
> `<role rolename="manager-gui"/>`
>
> `<role rolename="manager-script"/>`
>
> `<user username="admin" password="admin123" roles="manager-gui,manager-script"/>`
>
> username and password can be anything depending upon user and save it using `:wq`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135146.png)

------

> configure the webapps
>
> change directory to `cd webapps/manager/META-INF` and `ls` to list the file to be configured
>
> open editor `vi <file name>` here in below image it is `vi context.xml` 

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135243.png)

-------

> here remove the valve file

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135403.png)

----

> after removing it enter `:wq` to save the file 
>
> below image shows the configured file

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135427.png)

-----

> Now change directory to  `cd bin`
>
> `./shutdown.sh` shutdown the web server
>
> `./startup.sh` start the web server

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135513.png)

--------

> open the browser and refresh the browser it will ask username and password
>
> Enter the valid username and password while u have given in adding users 
>
> signin

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135529.png)

------

> Now after configuration you can access manager in web server 
>
> here you will see all the files present in webapps
>
> so our build code file is in build server , now you have to copy that file to DEPLOY server(webserver)

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135556.png)

-----

> open Powershell and change directory to where your PEM file is present (downloads) use `cd downloads`

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135616.png)

-------

> copy path of source(BUILD server)

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20135832.png)

-----

> copy path of destination(DEPLOY server)
>
> ![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20140003.png)

-----

> To copy from one server to another server you need to use SCP
>
> `scp -i pem.pem ubuntu@<source IP>:path ubuntu@<destination IP>:path`
>
> After this the BUILD CODE file in BUILD server is copied into webapps of the DEPLOY server

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20141223.png)

-----

> Open the browser and  you can see the .war file i.e /webapp-0.1.3
>
> click on that to see output

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20141300.png)

-------

> The Build code is successfully deployed 

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20141311.png)

-----

> Test the output

![](TOMCAT%20DEPLOY/Screenshot%202025-10-07%20141330.png)
