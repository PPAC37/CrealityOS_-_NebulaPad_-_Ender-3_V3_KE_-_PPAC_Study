

Exploration depuis le promt connecté en ssh utilisateur root
~~~
ssh 192.168.1.23 -l
~~~
On se retrouve normalement sur un truc qui resemble à
~~~
root@F005-4A88 /root [#] 
~~~

Note : Le nom d'hôte ici "F005-4A88" est la concatenation de "F005" (la Ender-3 V3 SE), du caractère "-", et des quatres dernier caractère de l'adresse MAC de la machine.


---

info systeme de fichier
~~~
mount
~~~
retourne

<pre>
root@F005-4A88 /root [#] mount
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
/dev/sda1 on /tmp/udisk/sda1 type vfat (rw,sync,relatime,fmask=0022,dmask=0022,codepage=936,iocharset=utf8,shortname=mixed,errors=remount-ro)
root@F005-4A88 /root [#]
</pre>

Pour mieux comprendre les sytemes de fichiers monté en "overlay" (en gros, une notion de supperposition de partitions. Une dite "lower" (en principe non modifiable) et une dite "upper" (pour les modifications effectuées) pour donner ici en "/" un systeme de fichier modifiable dont la coche "upper", "surcharge"/"masque"/"contient les modification de" la couche "lower" ... ) 
 - https://linuxconfig.org/introduction-to-the-overlayfs


---

Les "espaces disques" et partitions disponiblent
~~~
fdisk -l
~~~
retourne ( ici j'ai la clé USB de connecté ) 
<pre>
root@F005-4A88 /root [#] fdisk -l
Found valid GPT with protective MBR; using GPT

Disk /dev/mmcblk0: 15273600 sectors, 3361M
Logical sector size: 512
Disk identifier (GUID): 51254a50-067b-1d83-bde4-6c21babe3e1b
Partition table holds up to 11 entries
First usable sector is 34, last usable sector is 15271935

Number  Start (sector)    End (sector)  Size Name
     1            2048            4095 1024K ota
     2            4096            6143 1024K sn_mac
     3            6144           14335 4096K rtos
     4           14336           22527 4096K rtos2
     5           22528           38911 8192K kernel
     6           38912           55295 8192K kernel2
     7           55296         1079295  500M rootfs
     8         1079296         2103295  500M rootfs2
     9         2103296         2717695  300M rootfs_data
    10         2717696        15271935 6130M userdata
Disk /dev/mmcblk0boot1: 4 MB, 4194304 bytes, 8192 sectors
128 cylinders, 4 heads, 16 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Disk /dev/mmcblk0boot1 doesn't contain a valid partition table
Disk /dev/mmcblk0boot0: 4 MB, 4194304 bytes, 8192 sectors
128 cylinders, 4 heads, 16 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Disk /dev/mmcblk0boot0 doesn't contain a valid partition table
Disk /dev/sda: 15 GB, 15728640000 bytes, 30720000 sectors
1912 cylinders, 255 heads, 63 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Device  Boot StartCHS    EndCHS        StartLBA     EndLBA    Sectors  Size Id Type
/dev/sda1 *  0,1,2       1023,254,63         64   30719999   30719936 14.6G  c Win95 FAT32 (LBA)
root@F005-4A88 /root [#]
</pre>

---




<details>
 <summary>Si l'on veux faire une image de la partition, cela prend du temps ... (Cliquez pour déplier!)</summary>
Pour créer un fichier image de la partition mmcblk0p9 sur la clé USB (C'est trés long de l'ordre d'une heure ou deux heure car l'on copie tout le block même les block vides de cette partition de 500 MB)
~~~
dd if=/dev/mmcblk0p9 of=/tmp/udisk/sda1/dd_mmcblk0p9.img
~~~

Pour plus de détails sur l'utilisation de la commande `dd`

https://www.tecmint.com/clone-linux-partitions/


Faire une image de la partition dans un fichier sur `/usr/data` (point de montage de la partition mmcblk0p10) prend de l'ordre de 30 minutes.
~~~
dd if=/dev/mmcblk0p9 of=/usr/data/dd_mmcblk0p9.img
~~~
Mais ensuite la copie vers la clé USB prend de l'ordre d'une heure
~~~
mv /usr/data/dd_mmcblk0p9.img /tmp/udisk/sda1/
~~~
</details>





