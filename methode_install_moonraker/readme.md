



# https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Scripts/installer.sh
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

~~~



