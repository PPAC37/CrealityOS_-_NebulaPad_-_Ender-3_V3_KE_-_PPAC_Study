
Pré-requis
- firmware v1.1.0.12 mode root activé
- commande `opkg` fourni par Entware installable via le "[Helper Script Installation](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Helper-Script-Installation)" de Guilouz ( cf  [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Entware) )
~~~
cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
cd && sh ./installer.sh
~~~
Après avoir installé Entware, il faut soit exécuter la commande
~~~
export PATH="/opt/bin:/opt/sbin:$PATH"
~~~
soit se déconnecter et ré-ouvrir une connexion ssh (pour que la variable d'environnement PATH soit a jour car l'installation a placé un /etc/profile.d/entware.sh qui est automatiquement exécuté a l'ouverture d'une session.)

<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] opkg
-sh: opkg: not found
root@F005-4A88 /root [#] 

root@F005-4A88 /root [#] cat /etc/profile.d/entware.sh 
export PATH="/opt/bin:/opt/sbin:$PATH"
root@F005-4A88 /root [#] 

root@F005-4A88 /root [#] export PATH="/opt/bin:/opt/sbin:$PATH"
root@F005-4A88 /root [#] 

root@F005-4A88 /root [#] which opkg
/opt/bin/opkg
root@F005-4A88 /root [#] 

root@F005-4A88 /root [#] opkg list-installed
entware-opt - 227000-3
entware-release - 1.0-2
entware-upgrade - 1.0-1
findutils - 4.9.0-1a
grep - 3.8-2
libc - 2.27-11
libgcc - 8.4.0-11
libpcre2 - 10.42-1
libpthread - 2.27-11
librt - 2.27-11
libssp - 8.4.0-11
libstdcpp - 8.4.0-11
locales - 2.27-9
opkg - 2022-02-24-d038e5b6-2
terminfo - 6.4-2
zoneinfo-asia - 2023c-2
zoneinfo-core - 2023c-2
zoneinfo-europe - 2023c-2
root@F005-4A88 /root [#] 
</pre>
</details>

---

Utiliser `opkg` (fourni par Entware) pour installer les paquets suivants
~~~
opkg install mjpg-streamer
~~~
<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] opkg install mjpg-streamer
Installing mjpg-streamer (1.0.0-6) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/mjpg-streamer_1.0.0-6_mipsel-3.4.ipk
Installing libjpeg-turbo (2.1.4-2) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libjpeg-turbo_2.1.4-2_mipsel-3.4.ipk
Installing libiconv-full (1.17-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libiconv-full_1.17-1_mipsel-3.4.ipk
Installing libv4l (1.22.1-1) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/libv4l_1.22.1-1_mipsel-3.4.ipk
Configuring libiconv-full.
Configuring libjpeg-turbo.
Configuring libv4l.
Configuring mjpg-streamer.
root@F005-4A88 /root [#] 
</pre>
</details>

~~~
opkg install mjpg-streamer-input-uvc
~~~
<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
// A FAIRE
</pre>
</details>

~~~
opkg install mjpg-streamer-output-http
~~~
<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] opkg install mjpg-streamer-output-http
Installing mjpg-streamer-output-http (1.0.0-6) to root...
Downloading http://bin.entware.net/mipselsf-k3.4/mjpg-streamer-output-http_1.0.0-6_mipsel-3.4.ipk
Configuring mjpg-streamer-output-http.
root@F005-4A88 /root [#] ll /opt/lib/mjpg-streamer/
total 56
drwxr-xr-x    2 root     root          4096 Feb  6 02:09 ./
drwxr-xr-x    6 root     root          4096 Sep  1 21:07 ../
-rw-r--r--    1 root     root         12016 Sep  1 21:07 input_http.so
-rw-r--r--    1 root     root         35760 Sep  1 21:07 output_http.so
root@F005-4A88 /root [#] /etc/init.d/S50non_creality_webcam restart
killall: mjpg_streamer: no process killed
root@F005-4A88 /root [#] 
</pre>
</details>

Vérifier que votre Webcam se trouve bien connectée (Ici, j'ai une Logitech C170)
~~~
lsusb
~~~
<pre>
root@F005-4A88 /root [#] lsusb
Bus 001 Device 003: ID 046d:082b Logitech, Inc. Webcam C170
Bus 001 Device 002: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
root@F005-4A88 /root [#] 
</pre>


Vérifier que v4l (video for linux) trouve alors un périphérique vidéo
~~~
v4l2-ctl --list-devices
~~~
<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] v4l2-ctl --list-devices
jz-rot ():
	/dev/video0

Webcam C170 (1.2):
	/dev/media0

Dummy video device (0x0000) (platform:v4l2loopback-000):
	/dev/video3

Webcam C170 (usb-13500000.otg_new-1.2):
	/dev/video4

vpu-felix (vpu-felix):
	/dev/video2

vpu-helix (vpu-helix):
	/dev/video1

root@F005-4A88 /root [#] 
</pre>
</details>

Pour n'avoir que le/les périphériques vidéos dont on a besoin ici
~~~
v4l2-ctl --list-devices|grep -A1 usb|sed 's/^[[:space:]]*//g'|grep '^/dev'
~~~
Dans mon cas cela donne
<pre>
/dev/video4
</pre>


Pour connaitre les résolutions et format disponible pour ce périphérique vidéo ici `/dev/video4` (mais cela peut changer chez vous donc commande suivant a adapter au besoin)
~~~
v4l2-ctl -d /dev/video4 --list-formats-ext
~~~
<details>
 <summary>Résultat de la commande sur ma machine (Cliquez pour déplier!)</summary>
<pre>
root@F005-4A88 /root [#] v4l2-ctl -d /dev/video4 --list-formats-ext
ioctl: VIDIOC_ENUM_FMT
	Type: Video Capture

	[0]: 'YUYV' (YUYV 4:2:2)
		Size: Discrete 640x480
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 352x288
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 320x240
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 176x144
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 160x120
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 544x288
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 432x240
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 320x176
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 640x360
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
	[1]: 'MJPG' (Motion-JPEG, compressed)
		Size: Discrete 640x480
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 352x288
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 320x240
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 176x144
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 160x120
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 544x288
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 432x240
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 320x176
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 640x360
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 800x480
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
		Size: Discrete 1024x768
			Interval: Discrete 0.033s (30.000 fps)
			Interval: Discrete 0.067s (15.000 fps)
root@F005-4A88 /root [#] 
</pre>
</details>

---

Telecharger le script https://openk1.org/static/k1/scripts/multi-non-creality-webcams.sh
( mais là ma commande ne fonctionn pas ... ? http vs https ? , donc j'ai telechargé sur mon PC pour ensuite le transférer en `sftp` au préalable installé via `opkg` ...)
~~~
wget --no-check-certificate -O- 'https://openk1.org/static/k1/scripts/multi-non-creality-webcams.sh' > /etc/init.d/S50non_creality_webcam
~~~

ou copier coller le bloc suivant pour créé un fichier `/etc/init.d/S50non_creality_webcam` adapté pour ma Logitec C170 ( changement de la résolution cf `-r 640x360` )
~~~ bash
cat > /etc/init.d/S50non_creality_webcam<<'===EOF==='
#!/bin/sh
# S50non_creality_webcam - by destinal
# Start up mjpg-streamer on port 8080 for non-creality cameras (where cam_app doesn't autostart)

# Notes PPAC :
## Source de la version original de ce script :
# https://openk1.org/static/k1/scripts/multi-non-creality-webcams.sh
## pré-requis 
# - le résultat d'un "lsusb" doit avoir une ligne en plus quand on branche la Webcam sur l'un des ports USB du NebulaPad.
# - installer Entware via le script de Guilouz pour avoir la commande "opkg" cf https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Entware
# - opkg install mjpg-streamer
# - opkg install mjpg-streamer-input-uvc
# - opkg install mjpg-streamer-output-http
# - Adapter la resolution cf argument '-r' de mjpg_streamer ( cf "v4l2-ctl --list-devices|grep -A1 usb|sed 's/^[[:space:]]*//g'|grep '^/dev'" et "v4l2-ctl -d /dev/video4 --list-formats-ext" )
# Fin des notes de PPAC.

case "$1" in
  start)
    # V4L_DEV=$(v4l2-ctl --list-devices|grep -A1 usb|tail -1|sed 's/^[[:space:]]*//g')
    V4L_DEVS=$(v4l2-ctl --list-devices|grep -A1 usb|sed 's/^[[:space:]]*//g'|grep '^/dev')
    CREALITY_CAMS=$(v4l2-ctl --list-devices|grep CREALITY|wc -l)
    if [ "x$V4L_DEVS" = "x" -o $CREALITY_CAMS -gt 0 ]; then
      echo "No third party webcams found or we have a creality camera. Bailing!"
      exit 1
    fi

    # Otherwise we're all set up and have a device ID
    PORT=8080
    for V4L_DEV in $V4L_DEVS; do
      /opt/bin/mjpg_streamer -b -i "/opt/lib/mjpg-streamer/input_uvc.so -d $V4L_DEV -r 640x360 -f 15" -o "/opt/lib/mjpg-streamer/output_http.so -p $PORT"
      PORT=`expr $PORT + 1` 
    done
    ;;
  stop)
    killall mjpg_streamer
    ;;
  restart|reload)
    "$0" stop
    "$0" start
    ;;
  *)
    echo "Usage:"
    echo "    $0 {start|stop|restart}"
    exit 1
esac

exit $?
# Fin de mon ficher /etc/init.d/S50non_creality_webcam
===EOF===

~~~

rendre exécutable le fichier `/etc/init.d/S50non_creality_webcam` fraichement créé
~~~
chmod u+x /etc/init.d/S50non_creality_webcam
~~~



Lancer le sercice `/etc/init.d/S50non_creality_webcam` fraichement créé
~~~
/etc/init.d/S50non_creality_webcam restart
~~~
En principe s'il n'y avait pas de flux video déja servi par `/opt/bin/mjpg_streamer`, cela fait un message car la commande `killall mjpg_streamer` ne tue aucun processus. C'est normal.
<pre>
...
</pre>


Et là normalement l'on devrait obtenir un flux vidéo à l'adresse ( remplacer 192.168.1.23 par l'adresse IP de votre imprimante dans votre réseau local)
~~~
http://192.168.1.23:8080/?action=stream
~~~
ou 
~~~
http://192.168.1.23:4409/webcam/?action=stream
~~~

Il est normal d'obtenir un genre de message d'erreur a l'url [http://192.168.1.23:8080/](http://192.168.1.23:8080/) car l'on utilise pas l'url complète
<pre>
501: Not Implemented!
no www-folder configured
</pre>


Sous l'interface web de mainsail (http://192.168.1.23:4409) si installé, il peut y avoir besoin de supprimer et recrééer une webcam avec la config suivante : 
 - streaming URL
~~~
http://192.168.1.23:4409/webcam/?action=stream
~~~
 - snapshot URL
~~~
http://192.168.1.23:4409/webcam/?action=snapshot
~~~

---

---

Commandes à utiliser en cas de soucis

~~~
v4l2-ctl --all
~~~

~~~
ls -la /opt/lib/mjpg-streamer/
~~~
<pre>

</pre>

~~~
opkg install v4l-utils
~~~

---


Ressources :
 - Certains messages de l'utilisateur `destinal` sur https://www.reddit.com/r/Ender3V3KE/ et sur le serveur Discord [https://discord.gg/d3vil-design](https://discord.gg/d3vil-design)
