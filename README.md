# AWS BUILD SERVER CREATION

### LAUNCH EC2

> create a instance by giving instance name 



![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120405.png)

----



> select ubuntu image and make sure it is latest version i.e 24.04 LTS (HVM)

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120428.png)

----



> click on edit network settings and change security group name(optional) and launch instance

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120507.png)

----



> connect to the instance

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120622.png)

----



> copy the SSH key and open terminal 

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120636.png)

---



> In terminal change directory to downloads(your PEM file is present in downloads)

> use the below command:

> `cd downloads` and press enter

> paste the SSH key and press enter now it will ask permission yes/no type yes 

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120714.png)

-----



> Now you are connected to BUILD server image(ubuntu) 

![](C:\Users\jagan\OneDrive\Desktop\BUILD SERVER\Screenshot 2025-10-07 120731.png)



# JAVA BUILD-MAVEN 

#### GIT CLONE

 >Open the GITHUB repo where JAVA code is stored in browser

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121029.png)

-----

>Now copy the HTTPS URL(click on code down arrow to find the URL as shown in below image)

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121049.png)

-----

> Now in terminal:

> run `git clone <YOUR URL>` and your code is cloned(downloaded) in your BUILD server 
>
> use the following commands:
>
> `ls` - to view the list of folders in repo
>
> `cd <folder name>` - to change directory 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121131.png)

-----

> Again use `ls` to view the files/folders present in the code repo

> read the POM file by using `cat pom.xml` and we get to know build tool and JAVA version developer mentioned

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121220.png)

------

> Now update the system and install JAVA by using 
>
> `sudo apt update -y`
>
> `sudo apt install openjdk-17-jre-headless -y` 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121307.png)

-----

> After Installing JAVA now install maven using
>
> `sudo  apt install maven -y`

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121410.png)

------

> validate the CODE by using
>
> `mvn validate`

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121516.png)

----

> To build the code use this command:
>
> `mvn package` 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121536.png)

-----

> You will get build failure as we have downloaded latest version of JAVA and Developer mentioned JAVA 8 version in POM file 
>
> now FIX it (in real time the DEVELOPER will fix the POM file) 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121604.png)

-----

> I have Used CHATGPT to fix the POM file
>
> Below is the updated POM file now copy the updated POM file

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121856.png)

-----

>Now erase the pom.xml by using `>pom.xml` cmd
>
>Open vi editor using `vi pom.xml` and by pressing I paste the updated pom file inside it use `:wq` to save it

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121929.png)

--------

> Use `mvn clean` to remove the previous failed build

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 122020.png)

------

> Now run `mvn package` again with new updated pom.xml 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 121536.png)

---

> Build Success and code Build is completed 

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 122106.png)

-----

> To view the Artifact (.war) use `ls` and `cd target` ,`ls` again u can see .war file in red  

![](C:\Users\jagan\OneDrive\Desktop\maven BUILD\Screenshot 2025-10-07 122127.png)

--------

# AWS DEPLOY SERVER CREATION AND CONFIGURATION

#### LAUNCH EC2

> create an instance by giving instance name

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123614.png)

-----

> select image ubuntu latest version same as BUILD server and launch the server

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123752.png)

-----

>  configure inbound rules

> go to security and u will find inbound and outbound rules 

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123812.png)

----

>  select edit inbound rules to add port number of TOMCAT WEB Server

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123824.png)

----

>Add port number 8080 
>
>Type: custom TCP ; Port range: 8080 ; Source: Anywhere IPV4

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123849.png)

-----

> After adding inbound rule click save rules and it will show successfully modified

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123900.png)

-----

> copy the SSH key and open Terminal

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 123927.png)

-----

> Use `cd downloads` to get into PEM file location which is saved in downloads
>
> Now paste the SSH key and enter yes you will be connected to DEPLOY server

![](C:\Users\jagan\OneDrive\Desktop\deploy server\Screenshot 2025-10-07 124017.png)

----

# BUILD CODE DEPLOYMENT-TOMCAT WEB SERVER

> Update the server using `sudo apt -y update`
>
> Install JAVA latest version by using `sudo apt install openjdk-17-jre-headless -y`

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125258.png)

---

> Browse apache tomcat install and open the website
>
> copy the address(URL Link) of tar.gz(pgp,sha512) file

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125403.png)

----

> Use `wget <tar.gz link address>` to download the folder

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125433.png)

----

> By using `ls` u can find downloaded folder
>
> to extract the folder use `tar -xvf apache-tomcat-9.0.110.tar.gz` 

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125500.png)

------

> Use `ls` to see the extracted folder
>
> Change directory to extracted folder `cd <folder name>` 
>
> To see the files/folders inside extracted folder use `ls`

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125533.png)

------

> Now change directory to bin folder `cd bin`
>
> Start TOMCAT server using `./startup.sh`

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 125927.png)

----

> To check whether the web server is started or not copy the public ip of DEPLOY server 

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 130038.png)

----

>Open New Icognito window and paste your IP along with Web server port number i.e <your IP>:8080 in the image it is 
>
>Ex: 54.91.69.103:8080

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 130105.png)

---

> Your TOMCAT Web server is started and you can see in the below image

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 130119.png)

---

> Select master option in the above image and you will be redirected to the page which shows 403 error
>
> You have to configure the WEB server 

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 130129.png)

--------

> First add a user for WEB server to do that
>
> `ls` lists all the files/folders
>
> change directory to `cd conf/`  and `ls` to see all the files/folders present inside it
>
> open file using `vi <file name>` here in the below image it is `vi tomcat-users.xml`

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 134932.png)

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

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135146.png)

------

> configure the webapps
>
> change directory to `cd webapps/manager/META-INF` and `ls` to list the file to be configured
>
> open editor `vi <file name>` here in below image it is `vi context.xml` 

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135243.png)

-------

> here remove the valve file

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135403.png)

----

> after removing it enter `:wq` to save the file 
>
> below image shows the configured file

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135427.png)

-----

> Now change directory to  `cd bin`
>
> `./shutdown.sh` shutdown the web server
>
> `./startup.sh` start the web server

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135513.png)

--------

> open the browser and refresh the browser it will ask username and password
>
> Enter the valid username and password while u have given in adding users 
>
> signin

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135529.png)

------

> Now after configuration you can access manager in web server 
>
> here you will see all the files present in webapps
>
> so our build code file is in build server , now you have to copy that file to DEPLOY server(webserver)

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135556.png)

-----

> open Powershell and change directory to where your PEM file is present (downloads) use `cd downloads`

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135616.png)

-------

> copy path of source(BUILD server)

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 135832.png)

-----

> copy path of destination(DEPLOY server)
>
> ![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 140003.png)

-----

> To copy from one server to another server you need to use SCP
>
> `scp -i pem.pem ubuntu@<source IP>:path ubuntu@<destination IP>:path`
>
> After this the BUILD CODE file in BUILD server is copied into webapps of the DEPLOY server

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 141223.png)

-----

> Open the browser and  you can see the .war file i.e /webapp-0.1.3
>
> click on that to see output

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 141300.png)

-------

> The Build code is successfully deployed 

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 141311.png)

-----

> Test the output

![](C:\Users\jagan\OneDrive\Desktop\TOMCAT DEPLOY\Screenshot 2025-10-07 141330.png)



