# CrealityOS - NebulaPad - Ender-3 V3 KE - PPAC_Study

Mes notes sur le firmware CrealityOS de la Ender-3 V3 KE 

**En cours d'élaboration**

Mon sujet de découverte de la Ender-3 V3 KE sur le forum : https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/#comment-572037

### Autre sujets en relation avec le firmware de la Ender-3 V3 KE

https://www.lesimprimantes3d.fr/forum/topic/56971-obico-sur-ender-v3-ke/#comment-578771


## Firmware v1.1.0.12 

https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper/releases/tag/V1.1.0.12

### Activer le mode root pour pouvoir ensuite se connecter en SSH

( reprise de https://www.lesimprimantes3d.fr/forum/topic/56116-creality-ender-3-v3-ke-la-d%C3%A9couverte-avant-le-test/?do=findComment&comment=576232 )

Pour activer le mode root : https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/root%20guide/root%20tutorial.pdf
 * mot de passe par defaut : Creality2023

#### Se connectér en ssh

~~~
ssh <ip> -l root
~~~
après acception de la clé hôte et saisie du mot de passe root
~~~
//TODO
~~~

( une bonne pratique est de changer le mot de passe root, avec la commande 
~~~
passwd
~~~
et de bien noter le nouveau mot de passe pour ne pas le perdre
)

##### Installation de fluidd + 
// extrait du [README_en](https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/blob/main/fluidd/README_en) de https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex/tree/main/fluidd

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

### Bidouilles pour que le serveur web serve le fichier /usr/data/creality/userdata/history/print_history_record.json via `http://<ip>/downloads/humbnail/historyL.txt`


~~~
cat > S99t_hist_http<<'===EOF==='
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

( bien noter que le fait au début, de mettre entre quote la ligne qui permet d'identifier la fin du bloc, evite l'interprétation des caractères spéciaux, et variables. Attention forcement il ne faut pas que le coprs du bloc contienne une ligne identique a celle utilisé pour udentifier la fin du bloc (ici mise entre quote au début). cf https://stackoverflow.com/questions/6896025/echo-a-large-chunk-of-text-to-a-file-using-bash )

( bien noter que le lien symbolique doit etre fait apré le lancement du service `/etc/init.d/S99start_app.sh`, qui gère le fichier /usr/data/creality/userdata/history/print_history_record.json,  d'où le nom `S99t_hist_http.sh` alphabétiquement aprés `S99start_app.sh` )

~~~
chmod a+x /etc/init.d/S99t_hist_http.sh
~~~

(Normalement a chaque démarrage le lien symbolique sera créé par se service . Et donc on retrouve a l'url `http://<ip>/downloads/humbnail/historyL.txt` le contenu de `/usr/data/creality/userdata/history/print_history_record.json` )

## Dépôts de références

### Officiel par Creality (Le NebulaPad utilise un firmware basé sur Creality OS)

https://github.com/CrealityOfficial/Ender-3_V3_KE_Klipper

https://github.com/CrealityOfficial/Ender-3_V3_KE_Annex

### Firmware Sonic Pad et/ou les K1 ( basé sur Creality OS )

https://github.com/fran6p/SonicPad

https://github.com/Guilouz/Creality-K1-and-K1-Max
