
Sources :
 - https://www.reddit.com/r/Creality_3D_Official/comments/18e7u7z/comment/kiwt83y/
 - destinal (utilisateur reddit)  et son serveur Discord https://discord.gg/d3vil-design

# Pré-requis

- mode root
- avoir installé entware [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) pour disposé de `opkg` via le script d'aide a l'installiotn de Guilouz
~~~
cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
cd && sh ./installer.sh
~~~

Une fois opkg installé l'utiliser pour installer les pacjets suivants
~~~
opkg install mjpg-streamer
~~~
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


~~~
opkg install mjpg-streamer-input-uvc
~~~
<pre>

</pre>


~~~
opkg install mjpg-streamer-output-http
~~~
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


Vérifier que votre Webcam se trouve bien connectée
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


savoir si v4l arrive a utiliser ce périphérique, lister les périphériques vidéos
~~~
v4l2-ctl --list-devices
~~~
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


~~~
v4l2-ctl --list-devices|grep -A1 usb|sed 's/^[[:space:]]*//g'|grep '^/dev'
~~~
<pre>
root@F005-4A88 /root [#] v4l2-ctl --list-devices|grep -A1 usb|sed 's/^[[:space:]]*//g'|grep '^/dev'
/dev/video4
root@F005-4A88 /root [#] 
</pre>






Pour connaitre les résolutions et format disponible pour se périphérique vidéo
~~~
v4l2-ctl -d /dev/video4 --list-formats-ext
~~~
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



Telecharger le script https://openk1.org/static/k1/scripts/multi-non-creality-webcams.sh
( mais là ma commande ne fonctionn pas ... ? http vs https ? , donc j'ai telechargé sur mon PC pour ensuite le transférer en sftp au préalable installé via opkg ...)
~~~
wget --no-check-certificate -O- 'https://openk1.org/static/k1/scripts/multi-non-creality-webcams.sh' > /etc/init.d/S50non_creality_webcam
~~~
<pre>

</pre>

ou copier coller la commande pour créé une version adapté pour ma Logitec C170 ( changement de la résolution )
~~~ bash
cat > /etc/init.d/S50non_creality_webcam<<'===EOF==='
#!/bin/sh
# S50non_creality_webcam - by destinal
# Start up mjpg-streamer on port 8080 for non-creality cameras (where cam_app doesn't autostart)

# Notes PPAC : pré-requis 
# lsusb # Dois avoir une ligne en plus quand on branche la WebCam sur l'un des ports USB du NebulaPad
# ...
# EntWare via le script de Guillouze pour avoir opkg
# opkg install mjpg-streamer-input-uvc
# opkg install mjpg-streamer-output-http
# ... resolution

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
chmod u+x /etc/init.d/S50non_creality_webcam
~~~





~~~
/etc/init.d/S50non_creality_webcam restart
~~~
En principe si il n'y avais pas de flux déja disponible cela fait un message d'erreur car il n'y a aucun pracess a kill c'est normal.
<pre>
...
</pre>


Et là normalement l'on devrait obtenir un flux vidéo sur l'adresse ( remplécer 192.168.1.23 par l'ip de votre imprimante dans votre réseau local)
~~~
http://192.168.1.23:8080/?action=stream
~~~
ou 
~~~
http://192.168.1.23:4409/webcam/?action=stream
~~~
<pre>

</pre>



Si pas de flux sous mainsail il peut y avoir besoins de supprimer et réajouté la caméra avec la config suivante : 

streaming URL
~~~
http://192.168.1.23:4409/webcam/?action=stream
~~~

snapshot URL
~~~
http://192.168.1.23:4409/webcam/?action=snapshot
~~~



Commandes a utiliser en ca s de soucis
~~~
v4l2-ctl --all
~~~
~~~
ls -la /opt/lib/mjpg-streamer/
~~~
~~~
opkg install v4l-utils
~~~
