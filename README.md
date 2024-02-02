# CrealityOS - NebulaPad - Ender-3 V3 KE - PPAC_Study

Mes notes sur le firmware CrealityOS de la Ender-3 V3 KE


> [!WARNING]
> **En cours d'élaboration**


> [Reformulation d'un extrait de [https://github.com/fran6p/SonicPad/blob/main/Obico/obico-spad.md](https://github.com/fran6p/SonicPad/blob/main/Obico/obico-spad.md)]  
> Creality OS, le système d'exploitation (dérivé d'OpenWRT) de Creality n'utilise ni `systemd` pour le lancement de services ni `sudo` pour exécuter des commandes avec les droits root.  
> De plus les versions de Klipper, Moonraker sont âgées et sont modifiées pour prendre en compte les caractéristiques des matérielles (Tablettes Sonic Pad / Nebula Pad / K1, K1 Max, ...) de Creality.

> [!WARNING]
> Donc **ne pas mettre a jour moonraker ou Klipper/Klippy et cela même si les interface Fluidd ou Mainsail vous le propose.**
> Sinon cela risque très fortement de planter la machine et il vous faudra faire un reset de la machine voir faire un recovery du firmware.


- Mon sujet de découverte de la Ender-3 V3 KE sur le forum lesimprimantes3d.fr
  - [https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/#comment-572037](https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/#comment-572037)
- Autre sujets en relation avec le firmware de la Ender-3 V3 KE
  - [https://www.lesimprimantes3d.fr/forum/topic/56971-obico-sur-ender-v3-ke/#comment-578771](https://www.lesimprimantes3d.fr/forum/topic/56971-obico-sur-ender-v3-ke/#comment-578771)
  - [https://www.lesimprimantes3d.fr/forum/topic/57003-boulette-suite-maj-ender-3-v3-ke-firmware-11012-root%C3%A9-plantage-suite-mise-a-jour-de-klipper-via-linterface-fluidd/#comment-579230](https://www.lesimprimantes3d.fr/forum/topic/57003-boulette-suite-maj-ender-3-v3-ke-firmware-11012-root%C3%A9-plantage-suite-mise-a-jour-de-klipper-via-linterface-fluidd/#comment-579230)


## Firmware v1.1.0.12 Officiel qui dispose d'un mode root

- [https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper/releases/tag/V1.1.0.12](https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper/releases/tag/V1.1.0.12)


### Activer le mode root pour pouvoir ensuite se connecter en SSH

( reprise de [https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/?do=findComment&comment=576232](https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/?do=findComment&comment=576232) )

Pour activer le mode root : 
 * Via l'écran de contrôle (NebulaPad) de l'imprimante cf [https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/root%20guide/root%20tutorial.pdf](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/root%20guide/root%20tutorial.pdf)
 * mot de passe par defaut : Creality2023


#### Se connectér en ssh

~~~
ssh <ip> -l root
~~~
après acception de la clé hôte et saisie du mot de passe root
~~~
//TODO
~~~

Ou utiliser par exemple MobaXterm (Windows) ou SnowFlake (linux). (port 22 ( = ssh), utilisateur `root` mote de passe par defaut `Creality2023`)

( A noter que sftp n'est pas installé par défaut dans CrealityOS, donc dans un premier temps ( sauf aprés avoir installé `entware` qui permet d'avoir de mettre en place le gestionnaire de paquets `opkg` qui permet d'installer `sftp` sur la KE) il ne sera pas posible d'explorer l'arborécence de fichiers mais seulement d'utiliser le mode console ssh. )



( une bonne pratique est de changer le mot de passe root, avec la commande 
~~~
passwd
~~~
et de bien noter le nouveau mot de passe pour ne pas le perdre
)

---

~~~
cat /usr/data/creality/userdata/config/system_version.json
~~~
retourne
~~~
{
  "sys_version":"V1.1.0.12",
  "fw_version":"",
  "app_version":1,
  "hw_version":"F005",
  "hw1_version":"",
  "website":"www.creality.com"
}
~~~

---

~~~
cat /usr/data/creality/userdata/config/system_version.json | jq -r '.sys_version'
~~~
retourne
~~~
V1.1.0.12
~~~

---

~~~
df -h | grep /dev/mmcblk0p10 | awk {'print $3 " / " $2 " (" $4 " available)" '}
~~~
retourne
~~~
2.6G / 5.9G (3.0G available)
~~~

---

~~~
mount
~~~
retourne
~~~
/dev/root on /rom type squashfs (ro,relatime)
devtmpfs on /dev type devtmpfs (rw,relatime,size=100748k,nr_inodes=25187,mode=755)
proc on /proc type proc (rw,relatime)
devpts on /dev/pts type devpts (rw,relatime,gid=5,mode=620,ptmxmode=666)
tmpfs on /dev/shm type tmpfs (rw,relatime,mode=777)
tmpfs on /tmp type tmpfs (rw,relatime)
tmpfs on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
sysfs on /sys type sysfs (rw,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
/dev/mmcblk0p9 on /overlay type ext4 (rw,sync,relatime,block_validity,delalloc,barrier,user_xattr)
overlayfs:/overlay on / type overlay (rw,sync,noatime,lowerdir=/,upperdir=/overlay/upper,workdir=/overlay/work)
/dev/mmcblk0p10 on /usr/data type ext4 (rw,sync,relatime,block_validity,delalloc,barrier,user_xattr)
~~~

---


##### Installation de fluidd

// extrait du [README_en](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/fluidd/README_en) de [https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/tree/main/fluidd](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/tree/main/fluidd)

Instruction

Put the same level directory file ( fluidd ) in the root directory of the U disk

Copy the files ( fluidd.sh and fluidd.tar ) to directory ( /usr/data )
~~~
cp /tmp/udisk/sda1/fluidd/* /usr/data/
~~~

Install fluidd, moonraker and nginx
~~~
/usr/data/fluidd.sh install
~~~

unstall fluidd, moonraker and nginx
~~~
/usr/data/fluidd.sh unstall
~~~

Into fluidd

IP with 4408 port

eg, 192.168.1.1:4408


Warning: Monnraker running for a long time on the K1 series poses a risk of memory overflow

---

### Bidouilles 
pour que le serveur web serve le fichier /usr/data/creality/userdata/history/print_history_record.json via `http://<ip>/downloads/humbnail/historyL.txt`

Creation d'un service pour faire un lien symbolique du fichier .json que l'on veux rendre dispo par le serveur web pré-installé

Bien noter que le lien symbolique doit etre fait apré le lancement du service `/etc/init.d/S99start_app`, qui semble générer le fichier /usr/data/creality/userdata/history/print_history_record.json.  
D'où le nom `S99t_hist_http` alphabétiquement aprés `S99start_app` )

~~~
cat > /etc/init.d/S99t_hist_http<<'===EOF==='
#!/bin/sh
#

case "$1" in
  start)
        ln -s /usr/data/creality/userdata/history/print_history_record.json /tmp/creality/local_gcode/humbnail/historyL.txt
        ;;
  stop)
        ;;
  restart|reload)
        ;;
  *)
        echo "Usage: $0 {start|stop|restart}"
        exit 1
esac

exit $?
===EOF===

~~~

Bien noter que le fait, au début, de mettre entre quote la ligne qui permet d'identifier la fin du bloc, evite l'interprétation des caractères spéciaux, et variables. Attention forcement il ne faut pas que le coprs du bloc contienne une ligne identique a celle utilisé pour identifier la fin du bloc (ici mise entre quote au début). cf [https://stackoverflow.com/questions/6896025/echo-a-large-chunk-of-text-to-a-file-using-bash](https://stackoverflow.com/questions/6896025/echo-a-large-chunk-of-text-to-a-file-using-bash).

rendre executable le fichier créé
~~~
chmod a+x /etc/init.d/S99t_hist_http
~~~

et enfin executer le service 
~~~
/etc/init.d/S99t_hist_http start
~~~
ou relancer/rebooter le système
~~~
reboot
~~~

(Normalement a chaque démarrage le lien symbolique sera créé par se service. Et donc on retrouve a l'url `http://<ip>/downloads/humbnail/historyL.txt` le contenu de `/usr/data/creality/userdata/history/print_history_record.json` )

---

Pour créer un fichier `/root/.profile` pour avoir lors de l'ouverture d'une session l'espace disque diponible et quelques info en plus
(`~/.profile` automatiquement executé a l'ouverture d'une session)
~~~
cat > /root/.profile<<'===EOF==='
# Mon fichier ~/.profile automatiquement executé a l'ouverture d'une session

# Afficher l'espace utilisé par les fichiers .gcode et les logs
du -hc /usr/data/printer_data/gcodes/ /usr/data/printer_data/logs/ /usr/data/creality/userdata/log
echo -e "\n"

# Definition d'alias
# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# les connexion réseaux
#ifconfig
#echo -e "\n"

# les ports en ecoute
#netstat -tunle
#echo -e "\n"

###
# La suite sont des blocs (eventuellement adapté) de code piqué dans https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Scripts/installer.sh
# Merci Guilouz !


# La version de Creality OS
echo "CrealityOS `cat /usr/data/creality/userdata/config/system_version.json | jq -r '.sys_version'`"

# Afficher l'espace disque disponible
df -h | grep /dev/mmcblk0p10 | awk {'print $3 " / " $2 " (" $4 " available)" '}


#model=`/usr/bin/get_sn_mac.sh model`

white=`echo -en "\033[m"`
blue=`echo -en "\033[36m"`
cyan=`echo -en "\033[1;36m"`
yellow=`echo -en "\033[1;33m"`
green=`echo -en "\033[01;32m"`
darkred=`echo -en "\033[31m"`
red=`echo -en "\033[01;31m"`

printer_config="/usr/data/printer_data/config/printer.cfg"
macro_config="/usr/data/printer_data/config/gcode_macro.cfg"
klipper_extra_folder="/usr/share/klipper/klippy/extras/"
firmware_version="$(cat /usr/data/creality/userdata/config/system_version.json | jq -r '.sys_version')"

moonraker_folder="/usr/data/moonraker/"
nginx_folder="/usr/data/nginx/"
fluidd_folder="/usr/data/fluidd"

mainsail_folder="/usr/data/mainsail/"




check_folder() {
    local folder_path="$1"
    if [ -d "$folder_path" ]; then
        printf "${green}✓"
    else
        printf "${red}✗"
    fi
}


hr() {
    printf ' %s\n' '│                                                              │'
}


infoline() {
    local status=$1
    local text=$2
    local color=$3
    local max_length=66
    local total_text_length=$(( ${#status} + ${#text} ))
    local padding=$((max_length - total_text_length))
    printf " │   $color${status} ${white}${text}%-${padding}s${white}│ \n" ''
}


check_file() {
    local file_path="$1"
    if [ -f "$file_path" ]; then
        printf "${green}✓"
    else
        printf "${red}✗"
    fi
}

check_ipaddress() {
    eth0_ip=$(ip -4 addr show eth0 2>/dev/null | grep -o -E '(inet\s)([0-9]+\.){3}[0-9]+' | cut -d ' ' -f 2 | head -n 1)
    wlan0_ip=$(ip -4 addr show wlan0 | grep -o -E '(inet\s)([0-9]+\.){3}[0-9]+' | cut -d ' ' -f 2 | head -n 1)
    if [ -n "$eth0_ip" ]; then
        printf "$eth0_ip"
    elif [ -n "$wlan0_ip" ]; then
        printf "$wlan0_ip"
    else
        printf "xxx.xxx.xxx.xxx"
    fi
}

check_ipaddress
echo -e "\n"

check_connection() {
    eth0_ip=$(ip -4 addr show eth0 2>/dev/null | grep -o -E '(inet\s)([0-9]+\.){3}[0-9]+' | cut -d ' ' -f 2 | head -n 1)
    wlan0_ip=$(ip -4 addr show wlan0 | grep -o -E '(inet\s)([0-9]+\.){3}[0-9]+' | cut -d ' ' -f 2 | head -n 1)
    if [ -n "$eth0_ip" ]; then
        printf "$eth0_ip (ETHERNET)"
    elif [ -n "$wlan0_ip" ]; then
        printf "$wlan0_ip (WLAN)"
    else
        printf "xxx.xxx.xxx.xxx"
    fi
}

check_version() {
  file="/usr/data/creality/userdata/config/system_version.json"
  if [ -e "$file" ]; then
    cat "$file" | jq -r '.sys_version'
  else
    printf "N/A"
  fi
}

##
#    infoline "$(check_folder "$moonraker_folder")" 'Moonraker'
    infoline "$(check_folder "$moonraker_folder")" $moonraker_folder

## Nginx = serveur web, 
# les ports selon les serveur sont définie dans /usr/data/nginx/nginx/nginx.conf
# cat /usr/data/nginx/nginx/nginx.conf
#    infoline "$(check_folder "$nginx_folder")" 'Nginx'
    infoline "$(check_folder "$nginx_folder")" $nginx_folder

##
#    infoline "$(check_folder "$fluidd_folder")" 'Fluidd :4408'
    infoline "$(check_folder "$fluidd_folder")" "$fluidd_folder :4408"

##
#    infoline "$(check_folder "$mainsail_folder")" 'Mainsail :4409'
    infoline "$(check_folder "$mainsail_folder")" "$mainsail_folder :4409"

#    hr

# Fin de mon ficher ~/.profile
===EOF===

~~~

---

## Dépôts de références

- Officiel par Creality (Le NebulaPad utilise un firmware basé sur Creality OS)
  - [https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper](https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper)
  - [https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex)
- Firmware Sonic Pad et/ou les K1 ( basé sur Creality OS )
  - [https://github.com/fran6p/SonicPad](https://github.com/fran6p/SonicPad)
  - [https://github.com/Guilouz/Creality-K1-and-K1-Max](https://github.com/Guilouz/Creality-K1-and-K1-Max)    
    - [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Helper-Script-Installation](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Helper-Script-Installation)https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Helper-Script-Installation
      - ~~~
        cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
        cd && sh ./installer.sh
        ~~~
      - [https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Scripts/installer.sh](https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Scripts/installer.sh)


