Moonraker est une interface/API qui permetra a d'autre interface web ( comme fluidd ou mainsail ) de communiquer avec Klipper/Klippy.

Le plus simple c'est de passer par le Script d'aide a l'installation pour les K1 de Guilouz https://github.com/Guilouz/Creality-K1-and-K1-Max/

---


Mes notes en vrac pour eventuellement le faire sans l'aide du script de Guilouz 


extrait de https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Scripts/installer.sh
<pre>
download_URL="https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/"

moonraker_config="/usr/data/printer_data/config/moonraker.conf"
moonraker_config_URL="${download_URL}moonraker/moonraker.conf"
moonraker_folder="/usr/data/moonraker/"
moonraker_URL="${download_URL}moonraker/moonraker.tar"
</pre>

~~~
wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/moonraker/moonraker.tar -O /usr/data/moonraker.tar

wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/moonraker/moonraker.conf -O /usr/data/moonraker.conf

tar -C /usr/data/moonraker -xvf /usr/data/moonraker.tar
~~~



