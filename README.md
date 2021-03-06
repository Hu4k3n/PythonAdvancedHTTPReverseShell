# PythonAdvancedHTTPReverseShell
Advanced python HTTP reverse shell made for Hacking Competition purpose. I am not responsible of what you do with this tool or any consequence/damage that can occur if you use it for illegal purpose.

This reverse shell works on any network that have the port 80 open. That being said, It can be extremely usefull. It was tested in a closed network, not over the whole internet. However, It will work over the internet, all you have to do is change the variables values of "*ATTACKER_IP*" (AttackerSide.py) and "*ATTACKER_IP_URL*" (VictimSide.py). More details below.

### Language: ### 

- Tested in Python 3.6, should work in all Python 3 version.

### Limitations: ###

- Obviously, this is HTTP protocol, meaning it is possible for someone to intercept the request and read them in plain text. I encoded every request except for file transfer with Base64, but I should either implement HTTPS or a custom encrypting algorithm combined with Base64 for optimal purpose.
               
- This reverse shell has no implemented persistancy. This is, however, not a major issue if you use this for Hacking competition purpose...

- It is in python, meaning that you need to compile it to be sure that it will execute on any machine, regardless if python is installed or not. It is simple to do, just Google it. But if you are reading this right now, you probably already know how.

### Table of Contents: ###
- [*Setting up*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#setting-up-)
  - [*Attacker side script*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#attacker-side-script)
  - [*Victim side script*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#victim-side-script)
- [*Commands*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#Commands-)
  - [*Remotely upload a file to the victim side -> upload::{FILE_TO_UPLOAD_PATH}*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#upload)
  - [*Change the remote working directory of the victim side -> cd::{PATH}*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#cd)
  - [*Download a remote file to the attacker side -> get::{FILE_TO_GET_PATH}*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#get)
  - [*Scan the ports of remote machine on the victim side -> scan::{IP_TO_SCAN}::{PORT_1},{PORT_2},{PORT_N}*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#scan)
  - [*Take a screenshot of the victim desktop -> screens*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#screens)
  - [*Execute a file on the Victim machine -> exec::{FILE_TO_EXECUTE_PATH}::{FILE_TO_EXECUTE_ARGUMENTS}*](https://github.com/FanaticPythoner/PythonAdvancedHTTPReverseShell#exec)
  
# Installation

- Download the repository

- Install the requirements for the attacker side in the requirements_(AttackerSide).txt file (pip install -r requirements_(AttackerSide).txt)

- If you decided not to compile the VictimSide.py script, install the requirements for the victim side on the remote machine with the requirements_(VictimSide).txt file (pip install -r requirements_(VictimSide).txt)

- Happy Hacking.


# Setting up :

Here is what you need to do to setup your hacking environment beyond installation for both the attacker side and the victim side.
##### IMPORTANT NOTE: Once you have set up the AttackerSide.py and VictimSide.py scripts, you NEED to start the AttackerSide.py script first, otherwise the reverse shell wont work.

### Attacker Side script ###

For the Attacker Side, it's pretty straight foward: 
- At the top of the script, change the "*ATTACKER_IP*" variable for your IP address (or Domain name, you know what you have to do)
- Unless you do some port fowarding and change the default connection port of the Victim Side script and do other manipulations, the variable "*ATTACKER_PORT*" should stay with the value "*80*".

Here is what the top of the script shoud look like on a closed network :

![alt text](https://i.imgur.com/OtStUWN.jpg)

### Victim Side script ###
Again, I strongly recommand you to learn how and compile the VictimSide.py script with the dependencies before sending it to your victim, otherwhise the victim will need to have python will all the dependencies installed in his/her machine (which is unlikely). Eitherway, you will need to do this crazy hard step before doing anything:
- At the top of the script, change "*ATTACKER_IP_URL*" by the Domain name / IP address of the attacker. The 'http://' prefix is important.

Here is what the top of the script shoud look like on a closed network :

![alt text](https://i.imgur.com/4G42IUF.jpg)

# Commands :

Here are all the currently available custom commands in this Reverse Shell and their explanation.
##### IMPORTANT NOTE: The argument separator of every single custom command is the double double-dot (::).
##### OTHER IMPORTANT NOTE: All the standard shell commands of the remote machine will work with this shell, except the command 'CD', because you obviously cannot normally change the working directory of an executing script.

## Upload ##

Command to upload a file on the Attacker Side to the Victim Side current shell working directory. The syntax is :
- upload::{FILE_TO_UPLOAD_PATH}

#### Example:

Here, I will upload the file "python-3.7.1-installer.exe" located in the "SampleFiles" folder to the Victim machine. If it work, you will see a message telling you everything worked. If it failed, it would have also told you :

Attacker Side :
![alt text](https://i.imgur.com/WSRDQ5Q.jpg)

On the victim side, you can see that the file uploaded successfully :
![alt text](https://i.imgur.com/UaCknZa.jpg)

## CD ##

Command to walk through Victim Side OS. The syntax is :
- cd::{PATH}

#### Example:

Here, I will change the working directory from the Victim desktop to the current Drive Root. If it work, you will see a message telling you everything worked. If it failed, it would have also told you :

Attacker Side :
![alt text](https://i.imgur.com/b5dHgjB.jpg)

## Get ##

Command to download a file on the Victim machine to the Attacker machine. The syntax is :
- get::{FILE_TO_GET_PATH}

#### Example:

Here, I will download the file we uploaded on the Victim side earlier (python-3.7.1-installer.exe). If it work, you will see a message telling you everything worked. If it failed, it would have also told you :

Attacker Side :
![alt text](https://i.imgur.com/iTcWS8t.jpg)

The downloaded file is put in a directory named "files" in the same directory as the Attacker Script file : 
![alt text](https://i.imgur.com/HFKrEtw.jpg)

## Scan ##

Command to scan ports of a machine on the Victim network. The syntax is :
- scan::{IP_TO_SCAN}::{PORT_1},{PORT_2},{PORT_N}

#### Example:

Here, I will scan the ports 80, 443 and 22 of the IP address 192.168.51.79. If it work, you will see a message telling you everything worked. If it failed, it would have also told you :

Attacker Side :
![alt text](https://i.imgur.com/kCP789B.jpg)

## Screens ##

Command to take a screenshot in the JPEG format of the Victim machine. The syntax is :
- get::{FILE_TO_GET_PATH}

#### Example:

Here, I will simply take a screenshot of the Victim machine :

Attacker Side :
![alt text](https://i.imgur.com/C0I4ZNW.jpg)

The screenshot is put in a directory named "files" in the same directory as the Attacker Script file : 
![alt text](https://i.imgur.com/38VFHG4.jpg)

## Exec ##

Command to execute a file on the Victim machine. You can specify arguments. The syntax is :
- exec::{FILE_TO_EXECUTE_PATH}::{FILE_TO_EXECUTE_ARGUMENTS}

#### Example:

Here, I will simply execute the file we previously uploaded on the Victim machine desktop (python-3.7.1-installer.exe). If it work, you will see a message telling you everything worked. If it failed, it would have also told you :

##### IMPORTANT NOTE: Until the remote file you executed get closed, the Attacker Side Server will wait a response from the Victim Side. This can either be a good or bad thing (for example a script you execute remotely, you can tell when it's over), but it is what it is for now. If i see someone complaining about it I will fix it.

Attacker Side :
![alt text](https://i.imgur.com/lE4pecK.jpg)

On the victim side, you can see that the file executed successfully :
![alt text](https://i.imgur.com/gMnOyPA.jpg)
