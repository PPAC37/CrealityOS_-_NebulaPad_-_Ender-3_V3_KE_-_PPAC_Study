
Exploration depuis le promt connecté en ssh utilisateur root
~~~
ssh 192.168.1.23 -l
~~~
On se retrouve normalement sur un truc qui resemble à
<pre>
root@F005-4A88 /root [#] 
</pre>

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

Pour mieux comprendre les sytemes de fichiers monté en "overlay" (en gros, une notion de supperposition de partitions. Une dite "lower" (en principe non modifiable) et une dite "upper" (pour les modifications effectuées) pour donner ici en "/" un systeme de fichier modifiable dont la coche "upper", "surcharge"/"masque"/"contient les modification de" la couche "lower" ... ) voir par exemple https://linuxconfig.org/introduction-to-the-overlayfs


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

Pour créer un fichier image de la partition mmcblk0p9 sur la clé USB (C'est trés long de l'ordre d'une heure ou deux heures car l'on copie tout les block même les block vides de cette partition de 500 MB et la vitesse d'ecriture sur la clé USB fourni est très lente ... )


partition de 1 MB avec un lable "ota" (stock ???)
~~~
dd if=/dev/mmcblk0p1 of=/usr/data/dd_mmcblk0p1.img
~~~

partition de 1 MB avec un lable "sn_mac" (stock ???)
~~~
dd if=/dev/mmcblk0p2 of=/usr/data/dd_mmcblk0p2.img
~~~

partition de 4 MB avec un lable "rtos" (stock ???)
~~~
dd if=/dev/mmcblk0p3 of=/usr/data/dd_mmcblk0p3.img
~~~

partition de 4 MB avec un lable "rtos2" (stock ???)
~~~
dd if=/dev/mmcblk0p4 of=/usr/data/dd_mmcblk0p4.img
~~~

partition de 500 MB avec un lable "rootfs" (stock ???)
~~~
dd if=/dev/mmcblk0p7 of=/usr/data/dd_mmcblk0p7.img
~~~

partition de 500 MB avec un lable "rootfs2" (stock ???)
~~~
dd if=/dev/mmcblk0p8 of=/usr/data/dd_mmcblk0p8.img
~~~


partition de 300 MB avec un lable "rootfs_data" (stoke le upper et work )
~~~
dd if=/dev/mmcblk0p9 of=/tmp/udisk/sda1/dd_mmcblk0p9.img
~~~

Pour plus de détails sur l'utilisation de la commande `dd` voir par exemple https://www.tecmint.com/clone-linux-partitions/


Faire une image de la partition dans un fichier sur `/usr/data` (point de montage de la partition mmcblk0p10) prend de l'ordre de 30 minutes.
~~~
dd if=/dev/mmcblk0p9 of=/usr/data/dd_mmcblk0p9.img
~~~
Mais ensuite la copie vers la clé USB prend de l'ordre d'une heure
~~~
mv -v /usr/data/dd_mmcblk0p9.img /tmp/udisk/sda1/
~~~
~~~
mv -v /usr/data/dd_mmcblk0p*.img /tmp/udisk/sda1/
~~~

</details>

---

~~~
cat /usr/data/creality/userdata/config/system_version.json
~~~
retourne
<pre>
{
  "sys_version":"V1.1.0.12",
  "fw_version":"",
  "app_version":1,
  "hw_version":"F005",
  "hw1_version":"",
  "website":"www.creality.com"
}</pre>

---


~~~
root@F005-4A88 /root [#] which mount_mmc_ext4.sh 
/usr/bin/mount_mmc_ext4.sh
root@F005-4A88 /root [#] cat /usr/bin/mount_mmc_ext4.sh
#!/bin/sh

prg_name=$0
partition_name=$1
dev_path=$1
mount_path=$2

# 显示错误和使用方法并退出
usage_exit()
{
	echo $1 1>&2
	echo "usage: $prg_name partition_name/dev_path mount_path" 1>&2
	exit 1
}

# 显示错误并退出
error_exit()
{
	echo $1 1>&2
	exit 1
}

# 获得字符串中的第几个word
get_word()
{
    local str="$1"
    local n=$2
    local i=0

    for word in $str
    do
        if [ $i = $n ]; then
            echo $word
            return 0
        fi
        let i=i+1
    done

    return 1
}

# 判读是否为10进制数字
is_digital()
{
    local d=$1
    local tmp=$1

    let d=d+1 2>/dev/null
    if [ $d = $tmp ]; then
        return 1
    fi

    d=$tmp

    let d=d+0 2>/dev/null
    if [ $tmp != $d ]; then
        return 1
    fi

    return 0
}

if [ "$2" = "" ] || [ "$3" != "" ]; then
    usage_exit "args != 2"
fi

result=`which mke2fs`
if [ "$result" = "" ]; then
    error_exit "mke2fs not found"
fi

detect_dev=

while read line;
do
    line=`echo "$line" | grep mmcblk`
    if [ "$line" = "" ]; then
        continue
    fi

    str=`get_word "$line" 3`

    is_digital ${str#mmcblk}
    if [ $? != 0 ]; then
        continue
    fi

    dev=/dev/$str
    str=`fdisk -l $dev | grep $partition_name`
    if [ "$str" = "" ]; then
        continue
    fi

    tmp=`get_word "$str" 5`
    if [ "$tmp" = "" ]; then
	tmp=`get_word "$str" 4`
    fi

    if [ "$tmp" != "$partition_name" ]; then
        continue
    fi

    is_ok=0
    is_digital `get_word "$str" 0` && \
    is_digital `get_word "$str" 1` && \
    is_digital `get_word "$str" 2` && \
    is_ok=1

    if [ $is_ok != 1 ]; then
        continue
    fi

    detect_dev=${dev}p`get_word "$str" 0`
    break;
done < /proc/partitions

if [ "$detect_dev" = "" ]; then
    detect_dev=`readlink -f $dev_path`
    if [ "$detect_dev" = "" ]; then
        error_exit "mount mmc: $dev_path not valid"
    fi
fi

result=`mount | grep -e $detect_dev -e $mount_path`
if [ "$result" != "" ]; then
	error_exit "resource busy: $result" 
fi

mkdir -p $mount_path
if [ ! -e $mount_path ]; then
	error_exit "can't create mount path: $mount_path"
fi

fsck -y -t ext4 $detect_dev
mount -o sync -t ext4 $detect_dev $mount_path
if [ $? != 0 ]; then
    mke2fs $detect_dev
    mount -o sync -t ext4 $detect_dev $mount_path
fi
root@F005-4A88 /root [#]
~~~


---

Normalement on retrouve la valeur du Z-Offset dans le fichier
~~~
tail /usr/data/printer_data/config/printer.cfg
~~~
---


