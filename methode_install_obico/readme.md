Pour installer Obico

Il faut savoir que CrealityOS ne fourni pas la commande `bash` et car il se trouve basé sur un linux minimaliste et bidouillé par Creality, cela ne facilite pas les choses.

Le plus simple c'est surement de passer par le "Installation Helper Script" de Guilouz [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script
)  
pour pouvoir faire [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Obico](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Obico)

~~~
cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
cd && sh ./installer.sh
~~~
<pre>
 ┌──────────────────────────────────────────────────────────────┐
 │          INSTALLATION HELPER FOR CREALITY K1 SERIES          │
 │             Copyright © Cyril Guislain (Guilouz)             │
 ├──────────────────────────────────────────────────────────────┤
 │ /!\ ONLY USE THIS SCRIPT WITH FIRMWARE 1.3.2.1 AND ABOVE /!\ │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │  1) [Install] Menu                                           │ 
 │  2) [Remove] Menu                                            │ 
 │  3) [Customize] Menu                                         │ 
 │  4) [Backup & Restore] Menu                                  │ 
 │  5) [Tools] Menu                                             │ 
 │  6) [Informations] Menu                                      │ 
 │  7) [System] Menu                                            │ 
 │                                                              │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │  u) Check Script Updates                                     │ 
 │  q) Exit                                                     │ 
 │                                                              │
 │                                                       v4.4.1 │
 └──────────────────────────────────────────────────────────────┘

 Type your choice and validate with Enter: 1

 ┌──────────────────────────────────────────────────────────────┐
 │                       [ INSTALL MENU ]                       │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │ •ESSENTIALS:                                                 │ 
 │    1) Install Moonraker and Nginx                            │ 
 │    2) Install Fluidd (port 4408)                             │ 
 │    3) Install Mainsail (port 4409)                           │ 
 │    4) Install Supervisor Lite                                │ 
 │                                                              │
 │ •UTILITIES:                                                  │ 
 │    5) Install Entware                                        │ 
 │    6) Install Klipper Gcode Shell Command                    │ 
 │    7) Install Hostname Service                               │ 
 │    8) Install Host Controls Support                          │ 
 │                                                              │
 │ •IMPROVEMENTS:                                               │ 
 │    9) Install Klipper Adaptive Meshing & Purging             │ 
 │   10) Install Buzzer Support                                 │ 
 │   11) Install Nozzle Cleaning Fan Control                    │ 
 │   12) Install Fans Control Macros                            │ 
 │   13) Install Improved Shapers Calibrations                  │ 
 │   14) Install Useful Macros                                  │ 
 │   15) Install Save Z-Offset Macros                           │ 
 │   16) Install Screws Tilt Adjust Support                     │ 
 │                                                              │
 │ •CAMERA:                                                     │ 
 │   17) Install Moonraker Timelapse                            │ 
 │   18) Install Camera Settings Control                        │ 
 │                                                              │
 │ •REMOTE ACCESS AND AI DETECTION:                             │ 
 │   19) Install OctoEverywhere                                 │ 
 │   20) Install Obico                                          │ 
 │   21) Install Mobileraker Companion                          │ 
 │                                                              │
 ├──────────────────────────────────────────────────────────────┤
 │                                                              │
 │  b) Back to [Main Menu]                                      │ 
 │  q) Exit                                                     │ 
 │                                                              │
 └──────────────────────────────────────────────────────────────┘

 Type your choice and validate with Enter: 20
</pre>

Mais pour l'exercise et afin de mieux comprendre comment cela fonctionne, 
j'ai préféré étudier le "Installation Helper Script" (donc le fichier `installer.sh` dans sa version v4.4.0 ) de Guilouz pour le faire manuellement.

---

Pour faire l'équivalent manuellement

<!--
https://www.lesimprimantes3d.fr/forum/topic/56971-obico-sur-ender-v3-ke/?do=findComment&comment=579114
-->


Il y a besoin de la commande `curl` du dépôt de Guilouz (car celle disponible d'origine manque d'options ...)  
( c'est un pré-requis pour installer entware qui fourni opkg. opkg un genre de gestionnaire de paquet qui est un pré-requis pour installer obico ... )

~~~
wget -q --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/fixes/curl -O /tmp/curl >/dev/null 2>&1
chmod +x /tmp/curl >/dev/null 2>&1 & 
~~~

une fois que l'on a curl, Il y a besoins de la commande `opkg` fournis par entware que l'on installe via un script du dépôt de Guilouz

~~~
rm -rf /opt /usr/data/opt
mkdir -p /usr/data/opt
ln -nsf /usr/data/opt /opt
wget --no-check-certificate -O - "https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/entware/generic.sh" | /bin/sh
~~~

<details>
 <summary>Le script `generic.sh` en question (Cliquez pour déplier!)</summary>
~~~bash
#!/bin/sh

TYPE='generic'
#TYPE='alternative'

#|---------|-----------------------|---------------|---------------|---------------------|-------------------|-------------------|----------------------|-------------------|
#| ARCH    | aarch64-k3.10         | armv5sf-k3.2  | armv7sf-k2.6  | armv7sf-k3.2        | mipselsf-k3.4     | mipssf-k3.4       | x64-k3.2             | x86-k2.6          |
#| LOADER  | ld-linux-aarch64.so.1 | ld-linux.so.3 | ld-linux.so.3 | ld-linux.so.3       | ld.so.1           | ld.so.1           | ld-linux-x86-64.so.2 | ld-linux.so.2     |
#| GLIBC   | 2.27                  | 2.27          | 2.23          | 2.27                | 2.27              | 2.27              | 2.27                 | 2.23              |
#|---------|-----------------------|---------------|---------------|---------------------|-------------------|-------------------|----------------------|-------------------|

unset LD_LIBRARY_PATH
unset LD_PRELOAD

ARCH=mipselsf-k3.4
LOADER=ld.so.1
GLIBC=2.27

echo 'Info: Checking for prerequisites and creating folders...'
if [ -d /opt ]; then
    echo 'Warning: Folder /opt exists!'
else
    mkdir /opt
fi
# no need to create many folders. entware-opt package creates most
for folder in bin etc lib/opkg tmp var/lock
do
  if [ -d "/opt/$folder" ]; then
    echo "Warning: Folder /opt/$folder exists!"
    echo 'Warning: If something goes wrong please clean /opt folder and try again.'
  else
    mkdir -p /opt/$folder
  fi
done

echo 'Info: Opkg package manager deployment...'
URL=http://bin.entware.net/${ARCH}/installer
REPLACE_OPKG_MIRROR=0
/tmp/curl -s -L $URL/opkg --connect-timeout 10 -o /opt/bin/opkg >/dev/null 2>&1
if [ $? -ne 0 ]; then
  echo 'Warning: Trying mirrors.bfsu.edu.cn mirror repo...'
  URL=http://mirrors.bfsu.edu.cn/entware/${ARCH}/installer
  /tmp/curl -s -L $URL/opkg -o /opt/bin/opkg >/dev/null 2>&1
  REPLACE_OPKG_MIRROR=1
fi
chmod 755 /opt/bin/opkg
/tmp/curl -s -L $URL/opkg.conf -o /opt/etc/opkg.conf

if [ $REPLACE_OPKG_MIRROR = '1' ]; then
  sed -i "s,http://bin.entware.net/${ARCH},http://mirrors.bfsu.edu.cn/entware/${ARCH},g" /opt/etc/opkg.conf
fi

echo 'Info: Basic packages installation...'
/opt/bin/opkg update
if [ $TYPE = 'alternative' ]; then
  /opt/bin/opkg install busybox
fi
/opt/bin/opkg install entware-opt

# Fix for multiuser environment
chmod 777 /opt/tmp

for file in passwd group shells shadow gshadow; do
  if [ $TYPE = 'generic' ]; then
    if [ -f /etc/$file ]; then
      ln -sf /etc/$file /opt/etc/$file
    else
      [ -f /opt/etc/$file.1 ] && cp /opt/etc/$file.1 /opt/etc/$file
    fi
  else
    if [ -f /opt/etc/$file.1 ]; then
      cp /opt/etc/$file.1 /opt/etc/$file
    fi
  fi
done

[ -f /etc/localtime ] && ln -sf /etc/localtime /opt/etc/localtime

echo 'Info: Congratulations!'
echo 'Info: If there are no errors above then Entware was successfully initialized.'
echo 'Info: Add /opt/bin & /opt/sbin to $PATH variable'
echo 'Info: Add "/opt/etc/init.d/rc.unslung start" to startup script for Entware services to start'
if [ $TYPE = 'alternative' ]; then
  echo 'Info: Use ssh server from Entware for better compatibility.'
fi
echo 'Info: Found a Bug? Please report at https://github.com/Entware/Entware/issues'
~~~
</details>

Ce qui donne chez moi

<pre>
Connecting to raw.githubusercontent.com (185.199.109.133:443)
writing to stdout
Info: Checking for prerequisites and creating folders...
Warning: Folder /opt exists!
Warning: Folder /opt/bin exists!
Warning: If something goes wrong please clean /opt folder and try again.
Warning: Folder /opt/etc exists!
Warning: If something goes wrong please clean /opt folder and try again.
Warning: Folder /opt/lib/opkg exists!
Warning: If something goes wrong please clean /opt folder and try again.
Warning: Folder /opt/tmp exists!
Warning: If something goes wrong please clean /opt folder and try again.
Warning: Folder /opt/var/lock exists!
Warning: If something goes wrong please clean /opt folder and try again.
Info: Opkg package manager deployment...
-                    100% |******************************************************************************************************|  3222  0:00:00 ETA
written to stdout
Info: Basic packages installation...
Downloading http://bin.entware.net/mipselsf-k3.4/Packages.gz
Updated list of available packages in /opt/var/opkg-lists/entware
Installing entware-opt (227000-3) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/entware-opt_227000-3_all.ipk
Installing libgcc (8.4.0-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libgcc_8.4.0-11_mipsel-3.4.ipk
Installing libc (2.27-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libc_2.27-11_mipsel-3.4.ipk
Installing libssp (8.4.0-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libssp_8.4.0-11_mipsel-3.4.ipk
Installing libpthread (2.27-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libpthread_2.27-11_mipsel-3.4.ipk
Installing librt (2.27-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/librt_2.27-11_mipsel-3.4.ipk
Installing libstdcpp (8.4.0-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libstdcpp_8.4.0-11_mipsel-3.4.ipk
Installing entware-release (1.0-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/entware-release_1.0-2_all.ipk
Installing zoneinfo-core (2023c-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/zoneinfo-core_2023c-2_mipsel-3.4.ipk
Installing zoneinfo-asia (2023c-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/zoneinfo-asia_2023c-2_mipsel-3.4.ipk
Installing zoneinfo-europe (2023c-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/zoneinfo-europe_2023c-2_mipsel-3.4.ipk
Installing findutils (4.9.0-1a) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/findutils_4.9.0-1a_mipsel-3.4.ipk
Installing terminfo (6.4-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/terminfo_6.4-2_mipsel-3.4.ipk
Installing libpcre2 (10.42-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libpcre2_10.42-1_mipsel-3.4.ipk
Installing grep (3.8-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/grep_3.8-2_mipsel-3.4.ipk
Installing locales (2.27-9) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/locales_2.27-9_mipsel-3.4.ipk
Installing opkg (2022-02-24-d038e5b6-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/opkg_2022-02-24-d038e5b6-2_mipsel-3.4.ipk
Installing entware-upgrade (1.0-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/entware-upgrade_1.0-1_all.ipk
Configuring libgcc.
Configuring libc.
Configuring libssp.
Configuring libpthread.
Configuring librt.
Configuring terminfo.
Configuring libpcre2.
Configuring grep.
Configuring locales.
Entware uses separate locale-archive file independent from main system
Creating locale archive /opt/usr/lib/locale/locale-archive
Adding en_EN.UTF-8
Adding ru_RU.UTF-8
You can download locale sources from http://bin.entware.net/other/i18n_glib227.tar.gz
You can add new locales to Entware using /opt/bin/localedef.new
Configuring entware-upgrade.
Upgrade operations are not required.
Configuring opkg.
Configuring zoneinfo-core.
Configuring zoneinfo-europe.
Configuring zoneinfo-asia.
Configuring libstdcpp.
Configuring entware-release.
Configuring findutils.
Configuring entware-opt.
Info: Congratulations!
Info: If there are no errors above then Entware was successfully initialized.
Info: Add /opt/bin & /opt/sbin to $PATH variable
Info: Add "/opt/etc/init.d/rc.unslung start" to startup script for Entware services to start
Info: Found a Bug? Please report at https://github.com/Entware/Entware/issues
</pre>

Ne pas faire les "Info: ..." mais 

~~~
echo 'export PATH="/opt/bin:/opt/sbin:$PATH"' > /etc/profile.d/entware.sh
echo -e '#!/bin/sh\n/opt/etc/init.d/rc.unslung "$1"' > /etc/init.d/S50unslung
chmod 755 /etc/init.d/S50unslung
/etc/init.d/S50unslung start
~~~

Et normalement on a les pré-requis pour passer a l'installation de obico
~~~
cd /usr/data
git clone https://github.com/TheSpaghettiDetective/moonraker-obico.git moonraker-obico
cd moonraker-obico
sh ./scripts/install_creality.sh -k
~~~

Ce qui donne mais que j'ai pas terminé ( pas l'app sur mon smartphone ... )

<pre>
root@F005-4A88 /usr/data/moonraker-obico [#] sh ./scripts/install_creality.sh -k


          ,----..
         /   /   \
        /   .     :    ,---,      ,--,
       .   /   ;.  \ ,---.'|    ,--.'|                  ,---.
      .   ;   /  ` ; |   | :    |  |,                  '   ,'\
      ;   |  ; \ ; | :   : :    `--'_        ,---.    /   /   |
      |   :  | ; | ' :     |,-. ,' ,'|      /     \  .   ; ,. :
      .   |  ' ' ' : |   : '  | '  | |     /    / '  '   | |: :
      '   ;  \; /  | |   |  / : |  | :    .    ' /   '   | .; :
       \   \  ',  /  '   : |: | '  : |__  '   ; :__  |   :    |
        ;   :    /   |   | '/ : |  | '.'| '   | '.'|  \   \  /
         \   \ .'    |   :    | ;  :    ; |   :    :   `----'
          `---`      /    \  /  |  ,   /   \   \  /
                     `-'----'    ---`-'     `----'


================> Obico for Klipper (Moonraker-Obico) <================
###                                                                 ###
###                 * AI-Powered Failure Detection                  ###
###              * Free Remote Monitoring and Access                ###
###               * 25FPS High-Def Webcam Streaming                 ###
###                   * Free 4.9-Star Mobile App                    ###
###                                                                 ###
=======================================================================

###### Installing required system packages...

Installing python3 (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3_3.11.4-1_mipsel-3.4.ipk
Installing libpython3 (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libpython3_3.11.4-1_mipsel-3.4.ipk
Installing python3-base (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-base_3.11.4-1_mipsel-3.4.ipk
Installing libbz2 (1.0.8-1a) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libbz2_1.0.8-1a_mipsel-3.4.ipk
Installing zlib (1.2.13-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/zlib_1.2.13-1_mipsel-3.4.ipk
Installing python3-light (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-light_3.11.4-1_mipsel-3.4.ipk
Installing python3-asyncio (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-asyncio_3.11.4-1_mipsel-3.4.ipk
Installing python3-email (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-email_3.11.4-1_mipsel-3.4.ipk
Installing python3-cgi (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-cgi_3.11.4-1_mipsel-3.4.ipk
Installing python3-pydoc (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-pydoc_3.11.4-1_mipsel-3.4.ipk
Installing python3-cgitb (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-cgitb_3.11.4-1_mipsel-3.4.ipk
Installing python3-codecs (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-codecs_3.11.4-1_mipsel-3.4.ipk
Installing libffi (3.4.2-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libffi_3.4.2-2_mipsel-3.4.ipk
Installing python3-ctypes (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-ctypes_3.11.4-1_mipsel-3.4.ipk
Installing libgdbm (1.21-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libgdbm_1.21-2_mipsel-3.4.ipk
Installing python3-dbm (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-dbm_3.11.4-1_mipsel-3.4.ipk
Installing python3-decimal (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-decimal_3.11.4-1_mipsel-3.4.ipk
Installing python3-distutils (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-distutils_3.11.4-1_mipsel-3.4.ipk
Installing python3-logging (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-logging_3.11.4-1_mipsel-3.4.ipk
Installing liblzma (5.4.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/liblzma_5.4.4-1_mipsel-3.4.ipk
Installing python3-lzma (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-lzma_3.11.4-1_mipsel-3.4.ipk
Installing python3-multiprocessing (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-multiprocessing_3.11.4-1_mipsel-3.4.ipk
Installing libncursesw (6.4-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libncursesw_6.4-2_mipsel-3.4.ipk
Installing python3-ncurses (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-ncurses_3.11.4-1_mipsel-3.4.ipk
Installing libatomic (8.4.0-11) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libatomic_8.4.0-11_mipsel-3.4.ipk
Installing libopenssl (3.0.10-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libopenssl_3.0.10-1_mipsel-3.4.ipk
Installing ca-certificates (20230311-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/ca-certificates_20230311-1_all.ipk
Installing python3-openssl (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-openssl_3.11.4-1_mipsel-3.4.ipk
Installing libreadline (8.2-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libreadline_8.2-1_mipsel-3.4.ipk
Installing python3-readline (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-readline_3.11.4-1_mipsel-3.4.ipk
Installing libsqlite3 (3410200-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libsqlite3_3410200-1_mipsel-3.4.ipk
Installing python3-sqlite3 (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-sqlite3_3.11.4-1_mipsel-3.4.ipk
Installing python3-unittest (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-unittest_3.11.4-1_mipsel-3.4.ipk
Installing python3-urllib (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-urllib_3.11.4-1_mipsel-3.4.ipk
Installing libuuid (2.39-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libuuid_2.39-2_mipsel-3.4.ipk
Installing python3-uuid (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-uuid_3.11.4-1_mipsel-3.4.ipk
Installing python3-xml (3.11.4-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-xml_3.11.4-1_mipsel-3.4.ipk
Installing python3-pip (23.2.1-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/python3-pip_23.2.1-1_mipsel-3.4.ipk
Configuring libpython3.
Configuring python3-base.
Configuring libbz2.
Configuring zlib.
Configuring python3-light.
Configuring python3-email.
Configuring python3-urllib.
Configuring libatomic.
Configuring python3-pydoc.
Configuring liblzma.
Configuring python3-cgi.
Configuring python3-cgitb.
Configuring python3-decimal.
Configuring libuuid.
Configuring python3-uuid.
Configuring python3-xml.
Configuring libncursesw.
Configuring python3-ncurses.
Configuring python3-distutils.
Configuring python3-codecs.
Configuring python3-multiprocessing.
Configuring libreadline.
Configuring libffi.
Configuring python3-asyncio.
Configuring python3-ctypes.
Configuring libgdbm.
Configuring python3-dbm.
Configuring python3-logging.
Configuring python3-lzma.
Configuring libopenssl.
Configuring ca-certificates.
Configuring python3-openssl.
Configuring python3-readline.
Configuring libsqlite3.
Configuring python3-sqlite3.
Configuring python3-unittest.
Configuring python3.
Configuring python3-pip.
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
###### Creating python virtual environment for moonraker-obico...

/usr/lib/python3.8/site-packages/virtualenv.py:25: DeprecationWarning: The distutils package is deprecated and slated for removal in Python 3.12. Use setuptools or check PEP 632 for potential alternatives
  import distutils.sysconfig
/usr/lib/python3.8/site-packages/virtualenv.py:25: DeprecationWarning: The distutils.sysconfig module is deprecated, use sysconfig instead
  import distutils.sysconfig
Running virtualenv with interpreter /usr/bin/python3
Using base prefix '/usr'
/usr/lib/python3.8/site-packages/virtualenv.py:1039: DeprecationWarning: the imp module is deprecated in favour of importlib; see the module's documentation for alternative uses
  import imp
New python executable in /usr/data/moonraker-obico-env/bin/python3
Also creating executable in /usr/data/moonraker-obico-env/bin/python
Installing setuptools, pip, wheel...done.

=========================== Obico Server URL ===========================

Now tell us what Obico Server you want to link your printer to.
You can use a self-hosted Obico Server or the Obico Cloud. For more information, please visit: https://obico.io.
For self-hosted server, specify "http://server_ip:port". For instance, http://192.168.0.5:3334.

The Obico Server. Press 'enter' to accept the default [https://app.obico.io]: 


###### Creating config file /usr/data/printer_data/config/moonraker-obico.cfg ...

===================== Link Printer to Obico Server =====================
WARNING:sarge:No process found for Command('getconf LONG_BIT')

Now open the Obico mobile or web app. If your phone or computer is connected to the
same network as your printer, you will see this printer listed in the app. Click
"Link Now" and you will be all set!

If you need help, head to https://obico.io/docs/user-guides/klipper-setup

Waiting for Obico app to link this printer automatically...  press 'Enter' if you
want to link your printer using a 6-digit verification code instead.

\

Switch to using 6-digit verification code to link printer? [Y/n] y

### Switched to using 6-digit verification code to link printer. ###

To link to your Obico Server account, you need to obtain the 6-digit verification code
in the Obico mobile or web app, and enter the code below.

If you need help, head to https://obico.io/docs/user-guides/klipper-setup


Enter verification code (or leave it empty to abort): 

....

==== Failed to link. Did you enter an expired code? ====

If you keep getting this error, press ctrl-c to abort it and then run the following command to debug:
PYTHONPATH=/usr/data/moonraker-obico/scripts/..: /usr/data/moonraker-obico/scripts/../../moonraker-obico-env/bin/python3 -m moonraker_obico.link -c /usr/data/printer_data/config/moonraker-obico.cfg -d

Enter verification code (or leave it empty to abort): 

The process to link to your Obico Server account didn't finish.


To resume the linking process at a later time, run:

-------------------------------------------------------------------------------------------------
cd ~/moonraker-obico
./install.sh
-------------------------------------------------------------------------------------------------

Need help? Stop by:

- The Obico's help docs: https://obico.io/help/
- The Moonraker-Obico support channel: https://obico.io/discord-obico-klipper
- The Obico discord community: https://obico.io/discord/

root@F005-4A88 /usr/data/moonraker-obico [#] 
</pre>

Contrairement a ce qui est dit pour reprendre il faudrait plutôt faire 

~~~
cd /usr/data/moonraker-obico
sh ./scripts/install_creality.sh -k
~~~

---

