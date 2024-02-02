
EN COURS RE REALISATION !
INCOMPLET et NON fonctionnel.


basé sur [https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/tree/main/fluidd](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/tree/main/fluidd)

Attention bien notter que la version de Fluidd est une version "derty" / "sale" ( ce qui veut dire que c'est une version bidouillé par Creality et qu'il n'est pas recommandé de la mettre a jour car sinon on perd les bidouilles de Creality et elle ne sera plus adapté a l'environnement CrealityOS ...)


De plus l'archive `fluidd.tar` de `Ender-3_V3_KE_Annex` contient aussi nginx (serveur web) et moonraker (interface d'interaction avec klipper) 
qui sont elles aussi des versions bidouillées par creality pour fonctionner sur creality OS et avec le Klippy bidouillé de Creality.

Donc là encore, des versions a ne pas mettre a jour, au risque de planter la machine et d'avoir a faire un reset ou un recovery du firmware.

~~~

~~~

// ??? comme il y a la commande git d'installé par defaut sur CrealityOS, voir si pas plus simple de se faire un dépot github pour chaque composants afin de permetre une installation relativement facilité et une mise a jour ultérieur...
~~~
#cd /usr
#git clone ... /usr/data/...
#/usr/data/.../script_install.sh
#/usr/data/.../script_verif_install.sh
#/usr/data/.../script_uninstall.sh

# cd /usr/data/...; git pull
~~~


// TODO voir pour un script qui telecharge et déployer le truc sans avoir a passer par la clé USB
~~~
# wget -q --no-check-certificate https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/raw/main/fluidd/fluidd/fluidd.tar -O /usr/data/fluidd.tar >/dev/null 2>&1
# wget -q --no-check-certificate https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/raw/main/fluidd/fluidd/fluidd.sh -O /usr/data/fluidd.sh >/dev/null 2>&1
# chmod u+x /usr/data/fluidd.sh
# /usr/data/fluidd.sh install
~~~

//TODO voir pour un script de vérififcation
~~~
#
if [ -d /usr/data/nginx ]; then echo "/usr/data/nginx : OK existe." else echo "/usr/data/nginx : N'EXISTE PAS !" done
      #/usr/data/nginx /usr/data/moonraker /usr/data/fluidd         
~~~


https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/fluidd/README_en
~~~
Instruction

Put the same level directory file ( fluidd ) in the root directory of the U disk

Copy the files ( fluidd.sh and fluidd.tar ) to directory ( /usr/data )
cp /tmp/udisk/sda1/fluidd/* /usr/data/

Install fluidd, moonraker and nginx
/usr/data/fluidd.sh install

unstall fluidd, moonraker and nginx
/usr/data/fluidd.sh unstall

Into fluidd
IP with 4408 port
eg, 192.168.1.1:4408

Warning: Monnraker running for a long time on the K1 series poses a risk of memory overflow
~~~

https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/raw/main/fluidd/fluidd/fluidd.tar

https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/fluidd/fluidd/fluidd.sh
~~~bash
#!/bin/sh

if [ "x$1" = "xinstall" ]; then
    cd /usr/data
    tar -xvf fluidd.tar 

    [ ! -e /etc/init.d/S50nginx ] && mv nginx/S50nginx /etc/init.d/
    [ ! -e /etc/init.d/S56moonraker_service ] && mv moonraker/S56moonraker_service /etc/init.d/

    /etc/init.d/S50nginx start
    /etc/init.d/S56moonraker_service start
elif [ "x$1" = "xunstall" ]; then
    cd /overlay/upper
    /etc/init.d/S50nginx stop
    /etc/init.d/S56moonraker_service stop
    rm -rf /etc/init.d/S50nginx /etc/init.d/S56moonraker_service 
    rm -rf /usr/data/printer_data/config/moonraker.conf /usr/data/printer_data/config/.moonraker.conf.bkp /usr/data/nginx /usr/data/moonraker /usr/data/fluidd
fi
~~~


