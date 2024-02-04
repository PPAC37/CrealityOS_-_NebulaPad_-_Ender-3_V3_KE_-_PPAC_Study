
Pré-requis :
- Avoir un compte https://octoeverywhere.com/

Le plus simple c'est surement de passer par le "Installation Helper Script" de Guilouz [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script
)  

~~~
cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
cd && sh ./installer.sh
~~~

---

Sinon en manuel 

~~~
cd /usr/data
git clone https://github.com/QuinnDamerell/OctoPrint-OctoEverywhere.git octoeverywhere
cd octoeverywhere
sh ./install.sh
~~~
<details>
 <summary>Ce qui donne chez moi ... (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] cd /usr/data
root@F005-4A88 /usr/data [#] git clone https://github.com/QuinnDamerell/OctoPrint-OctoEverywhere.git octoeverywhere
Cloning into 'octoeverywhere'...
remote: Enumerating objects: 1588, done.
remote: Counting objects: 100% (851/851), done.
remote: Compressing objects: 100% (289/289), done.
remote: Total 1588 (delta 662), reused 708 (delta 560), pack-reused 737
Receiving objects: 100% (1588/1588), 701.77 KiB | 1.23 MiB/s, done.
Resolving deltas: 100% (1077/1077), done.
root@F005-4A88 /usr/data [#] cd octoeverywhere
root@F005-4A88 /usr/data/octoeverywhere [#] sh ./install.sh

      @@@@@@@@@@@@@@@@@@@@@@@@***@@@@@@@@@@@@@@@@@@@@@@@
      @@@@@@@@@@@@@@***********************@@@@@@@@@@@@@
      @@@@@@@@@@*******************************@@@@@@@@@
      @@@@@@@@***********************************@@@@@@@
      @@@@@,,,************************/////////*****@@@@
      @@@@,,,,,,*****************//////////////******@@@
      @@,,,,,,,,,,***********//////////////////*******@@
      @@,,,,,,,,,,,,*******////////****///////*********@
      @,,,,,,,,,,,/////////////////****//////***********
      @,,,,,,,//////////////////////////////************
      ,,,,,,,,////////////////////////////**************
      @,,,,,,,,,,,,/////////////////////****************
      @,,,,,,,,,,,,,,/////////////////******************
      @@,,,,,,,,,,,,,,,,//////////////*****************@
      @@@,,,,,/#######,,,,///////////*****************@@
      @@@@,,,##########,,,,,,,//////,****************@@@
      @@@@@,##########,,,,,,,,,////,,,,*************@@@@
      @@@@@########,,,,,,,,,,,,//,,,,,,,,********@@@@@@@
      @@@@@#@@@@,,,,,,,,,,,,,,,,,,,,,,,,,,,***,@@@@@@@@@
      @@@@@@@@@@@@@@@,,,,,,,,,,,,,,,,,,,,,@@@@@@@@@@@@@@

                  OctoEverywhere For Klipper
 The 3D Printing Communities #1 Remote Access And AI Cloud Service


OctoEverywhere empowers the worldwide maker community with...
  - Free & Unlimited Mainsail and Fluidd Remote Access
  - Free & Unlimited Next-Gen AI Print Failure Detection
  - Free Full Frame Rate & Full Resolution Webcam Streaming
  - 5 Star Rated iOS & Android Apps
  - Real-Time Print Notifications
  - And So Much More


Running in K1 and K1 Max OS mode
Checking required system packages are installed...
Requirement already satisfied: virtualenv in /usr/lib/python3.8/site-packages (15.1.0)
System package install complete.
Checking Python Virtual Environment For OctoEverywhere...
No virtual environment found, creating one now.
Already using interpreter /usr/bin/python3
Using base prefix '/usr'
/usr/lib/python3.8/site-packages/virtualenv.py:1039: DeprecationWarning: the imp module is deprecated in favour of importlib; see the module's documentation for alternative uses
  import imp
New python executable in /usr/data/octoeverywhere-env/bin/python3
Also creating executable in /usr/data/octoeverywhere-env/bin/python
Installing setuptools, pip, wheel...done.
Updating PIP if needed... (this can take a few seconds or so)
Requirement already satisfied: pip in /usr/data/octoeverywhere-env/lib/python3.8/site-packages (23.3.2)
Installing or updating required python libs...
Python libs installed.
Bootstrap done. Starting python installer...
Os Type Detected: OsTypes.K1
Ensuring that time sync is enabled...

Only one moonraker instance was found, so we are using it! [S56moonraker_service:/usr/data/printer_data/config/moonraker.conf]
Starting configuration...
Enuring path and permissions [/usr/data/printer_data/octoeverywhere-store]...
Dir doesn't exist, creating...
Setting owner permissions to the service user [root]...
Directory setup successfully.
Configured. Service: S66octoeverywhere_service, Path: /etc/init.d/S66octoeverywhere_service, LocalStorage: /usr/data/printer_data/octoeverywhere-store, Config Dir: /usr/data/printer_data/config, Logs: /usr/data/printer_data/logs
Starting Web Interface Setup

The following web interfaces were automatically discovered:
  1) Fluidd   - Port 4408
  2) Mainsail - Port 4409
  3) Creality - Port 80

Enter the number next to the web interface you would like to use, or enter `m` to manually setup the web interface: 1
Setting Up OctoEverywhere's System Service...
Creating service run script...
Making the run script executable...
Creating service file /etc/init.d/S66octoeverywhere_service...
Making the service executable...
Starting the service...
Service setup and start complete!
Waiting for the plugin to produce a printer id... (this can take a few seconds)


You're 10 seconds away from free and unlimited printer access from anywhere!
To securely link this printer to your OctoEverywhere account, go to the following website and use the code.

Website: https://octoeverywhere.com/code
Code:    ******


Waiting for the printer to be linked to your account...

Success! This printer is securely connected to your account as 'E3V3KE_PPAC'

        ~~~ OctoEverywhere For Klipper Setup Complete ~~~    
  You Can Access Your Printer Anytime From OctoEverywhere.com
                   Welcome To Our Community                  
                            ❤️                               


root@F005-4A88 /usr/data/octoeverywhere [#] 
</pre>
</details>

Et si tout c'est bien passé vous devrez pouvoir vous connecter via une url de la forme https://nom_de_machine.octoeverywhere.com/#/

<!--
https://e3v3ke_ppac.octoeverywhere.com/#/
-->
