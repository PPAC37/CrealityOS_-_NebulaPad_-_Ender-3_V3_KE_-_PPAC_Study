
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

