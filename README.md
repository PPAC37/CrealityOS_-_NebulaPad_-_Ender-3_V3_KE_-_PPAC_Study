# CrealityOS - NebulaPad - Ender-3 V3 KE - PPAC_Study

Mes notes sur le firmware v1.1.0.12 (Creality OS) de la Ender-3 V3 KE


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
cat /usr/data/creality/userdata/config/system_version.json | jq -r '.sys_version'
~~~
retourne
<pre>
V1.1.0.12
</pre>

---

~~~
df -h | grep /dev/mmcblk0p10 | awk {'print $3 " / " $2 " (" $4 " available)" '}
~~~
retourne un truc de la forme
<pre>
2.6G / 5.9G (3.0G available)
</pre>


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


