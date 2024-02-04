
---

<pre>
root@F005-4A88 /root [#] cat /usr/share/script/recovery.sh
cat: can't open '/usr/share/script/recovery.sh': No such file or directory
root@F005-4A88 /root [#]
</pre>

<pre>
root@F005-4A88 /root [#] which curl
/usr/bin/curl
root@F005-4A88 /root [#]
</pre>

<pre>
root@F005-4A88 /root [#] which bash
root@F005-4A88 /root [#] 
</pre>

---

<pre>
root@F005-4A88 /root [#] ls -lah /usr/data/
total 265M   
drwxr-xr-x   10 root     root        4.0K Mar  1  2020 .
drwxr-xr-x    1 root     root        1.0K Feb  2 16:23 ..
drwxr-xr-x    4 root     root        4.0K Mar  1  2020 creality
-rw-r--r--    1 root     root          26 Mar  1  2020 factory_test_result
drwxr-xr-x    6 1014     1014        4.0K Feb  2 16:23 fluidd
-rwxr-xr-x    1 root     root         682 Feb  2 16:23 fluidd.sh
-rwxr-xr-x    1 root     root       80.8M Feb  2 16:23 fluidd.tar
drwx------    2 root     root        4.0K Mar  1  2020 lost+found
-rw-r--r--    1 root     root          18 Mar  1  2020 macaddr.txt
drwxr-xr-x    5 1014     1014        4.0K Feb  2 16:25 mainsail
-rwxr-xr-x    1 root     root         686 Feb  2 16:25 mainsail.sh
-rwxr-xr-x    1 root     root       56.1M Feb  2 16:25 mainsail.tar
drwxrwxr-x    4 1014     1014        4.0K Feb  2 16:25 moonraker
drwxrwxr-x    5 1014     1014        4.0K Feb  2 16:25 nginx
drwxr-xr-x   13 root     root        4.0K Sep  1 21:07 opt
drwxr-xr-x    8 root     root        4.0K Feb  2 16:24 printer_data
-rw-------    1 root     root      128.0M Mar  1  2020 swap
-rw-r--r--    1 root     root         174 Mar  1  2020 wpa_supplicant.conf
root@F005-4A88 /root [#]
</pre>

---

~~~
du -hc /usr/data/printer_data/logs/ /usr/data/creality/userdata/log/
~~~
<pre>
root@F005-4A88 /root [#] du -hc /usr/data/printer_data/logs/ /usr/data/creality/userdata/log/
6.4M	/usr/data/printer_data/logs/
101.2M	/usr/data/creality/userdata/log/
107.7M	total
root@F005-4A88 /root [#] 
</pre>


~~~
rm -v /usr/data/creality/userdata/log/*.gz /usr/data/printer_data/logs/*.log.*
~~~
<pre>
...
root@F005-4A88 /root [#] 
</pre>

~~~
du -hc /usr/data/printer_data/logs/ /usr/data/creality/userdata/log/
~~~
<pre>
root@F005-4A88 /root [#] du -hc /usr/data/printer_data/logs/ /usr/data/creality/userdata/log/
132.0K	/usr/data/printer_data/logs/
92.9M	/usr/data/creality/userdata/log/
93.0M	total
root@F005-4A88 /root [#] 
</pre>

---

~~~
ls -la /usr/data/printer_data/logs/
~~~
<pre>
root@F005-4A88 /root [#] ls -la /usr/data/printer_data/logs/
total 6580
drwxr-xr-x    2 root     root          4096 Feb  4 14:09 .
drwxr-xr-x    8 root     root          4096 Feb  2 16:24 ..
-rw-r--r--    1 root     root         55048 Feb  4 14:09 klippy.log
-rw-r--r--    1 root     root        150894 Mar  1  2020 klippy.log.2020-03-01
-rw-r--r--    1 root     root       6161290 Mar  1  2020 klippy.log.2024-02-02
-rw-r--r--    1 root     root        144041 Mar  1  2020 klippy.log.2024-02-03
-rw-r--r--    1 root     root         62376 Mar  1  2020 moonraker.log
-rw-r--r--    1 root     root        107420 Feb  2 23:22 moonraker.log.2024-02-02
root@F005-4A88 /root [#] 
</pre>

~~~
ls -la /usr/data/creality/userdata/log
~~~
<pre>
root@F005-4A88 /root [#] ls -la /usr/data/creality/userdata/log
total 96492
drwxr-xr-x    2 root     root          4096 Feb  2 18:52 ./
drwxr-xr-x    7 root     root          4096 Feb  2 19:11 ../
-rw-r--r--    1 root     root           323 Mar  1  2020 Monitor.log
-rw-r--r--    1 root     root       5324803 Feb  2 23:42 app-server.log
-rw-r--r--    1 root     root         30942 Mar  1  2020 audio-server.log
-rw-r--r--    1 root     root          1190 Mar  1  2020 cx_ai_middleware.log
-rw-r--r--    1 root     root          5414 Mar  1  2020 device_manager.log
-rw-r--r--    1 root     root      26715633 Feb  2 23:42 display-server.log
-rw-r--r--    1 root     root           157 Feb  2 16:04 log_config.json
-rw-r--r--    1 root     root      52201632 Feb  2 23:42 master-server.log
-rw-r--r--    1 root     root       5567643 Feb  2 18:52 master-server.log.1.gz
-rw-r--r--    1 root     root          6529 Mar  1  2020 upgrade-server.log
-rw-r--r--    1 root     root       6441247 Feb  2 23:42 web-server.log
-rw-r--r--    1 root     root          7438 Mar  1  2020 webrtc.log
-rw-r--r--    1 root     root       2332059 Feb  2 23:42 wifi-server.log
</pre>

~~~
cat /usr/data/creality/userdata/log/log_config.json
~~~
<pre>
root@F005-4A88 /root [#] cat /usr/data/creality/userdata/log/log_config.json 
{
  "#log_level":"LOG_DEFAULT=0, LOG_DEBUG=1, LOG_INFO=2, LOG_WARNING=3, LOG_ERROR=4",
  "log_level":1,
  "#log_route":"file=1, console=0",
  "log_route":1
}
</pre>

~~~
cat /etc/init.d/S99start_app
~~~
<pre>
root@F005-4A88 /root [#] cat /etc/init.d/S99start_app 
</pre>
~~~bash
#!/bin/sh
export TSLIB_CONFFILE=/etc/ts.conf
export TSLIB_TSDEVICE=/dev/input/event0
export TSLIB_FBDEVICE=/dev/fb0
export TSLIB_PLUGINDIR=/usr/lib/ts

BIN_PATH=/usr/bin
MASTER_SERVER=master-server
AUDIO_SERVER=audio-server
WIFI_SERVER=wifi-server
APP_SERVER=app-server
DISPLAY_SERVER=display-server
UPGRADE_SERVER=upgrade-server
WEB_SERVER=web-server
MONITOR=Monitor
DELAY_IMAGE_VIDEO_DIR=/usr/data/creality/userdata/delay_image/video
LOG_DIR=/usr/data/creality/userdata/log
FRONTEND_DOWNLOADS_DIR=/usr/share/frontend/downloads
HUMBNAIL_DIR=/tmp/creality/local_gcode/humbnail
ORIGINAL_DIR=/tmp/creality/original
DEFDATA_DIR=/etc/sysConfig/defData

stop_boot_display(){
    kill -9 $(ps | grep boot_display | grep -v grep | awk '{printf $1" "}')
}

clean_old_logs(){
    [ -d $LOG_DIR ] && rm -rf $LOG_DIR/*logfile*
}

start_server(){
    [ -d $FRONTEND_DOWNLOADS_DIR ] ||  mkdir -p $FRONTEND_DOWNLOADS_DIR
    [ -d $HUMBNAIL_DIR ] || mkdir -p $HUMBNAIL_DIR
    [ -d $ORIGINAL_DIR ] || mkdir -p $ORIGINAL_DIR
    [ -d $DELAY_IMAGE_VIDEO_DIR ] || mkdir -p $DELAY_IMAGE_VIDEO_DIR
    [ -d $FRONTEND_DOWNLOADS_DIR -a -d $HUMBNAIL_DIR -a -d $ORIGINAL_DIR -a -d $DEFDATA_DIR ]\
         && { ln -s $ORIGINAL_DIR $FRONTEND_DOWNLOADS_DIR; ln -s $HUMBNAIL_DIR $FRONTEND_DOWNLOADS_DIR;\
         ln -s $DEFDATA_DIR $FRONTEND_DOWNLOADS_DIR; ln -s $DELAY_IMAGE_VIDEO_DIR $FRONTEND_DOWNLOADS_DIR;}

    clean_old_logs

    export HOME=/root
    # sleep 2s # 应用进程延时启动，等待marlin先启动完成
    sync && echo 3 > /proc/sys/vm/drop_caches
    [ -x "$BIN_PATH/$MASTER_SERVER" ] && $BIN_PATH/$MASTER_SERVER &
    # sleep 2s # 主动进程启动后延时，等待获取marlin状态完成
    [ -x "$BIN_PATH/$AUDIO_SERVER" ] && $BIN_PATH/$AUDIO_SERVER &
    [ -x "$BIN_PATH/$WIFI_SERVER" ] && $BIN_PATH/$WIFI_SERVER &
    [ -x "$BIN_PATH/$APP_SERVER" ] && $BIN_PATH/$APP_SERVER &
    [ -x "$BIN_PATH/$DISPLAY_SERVER" ] && $BIN_PATH/$DISPLAY_SERVER &
    [ -x "$BIN_PATH/$UPGRADE_SERVER" ] && $BIN_PATH/$UPGRADE_SERVER &
    [ -x "$BIN_PATH/$WEB_SERVER" ] && $BIN_PATH/$WEB_SERVER &
    # 守护进程排在最后启动
    [ -x "$BIN_PATH/$MONITOR" ] && $BIN_PATH/$MONITOR &
}

stop_server(){
    killall $MONITOR
    killall $DISPLAY_SERVER
    killall $WIFI_SERVER
    killall $APP_SERVER
    killall $AUDIO_SERVER
    killall $MASTER_SERVER
    killall $UPGRADE_SERVER
    killall $WEB_SERVER
}

# stop_boot_display

case "$1" in
    start)
        start_server
        ;;
    stop)
        stop_server
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
~~~

~~~
rm -v /usr/data/creality/userdata/log/*.gz
~~~
<pre>
root@F005-4A88 /root [#] rm -v /usr/data/creality/userdata/log/*.gz
removed '/usr/data/creality/userdata/log/master-server.log.1.gz'
removed '/usr/data/creality/userdata/log/master-server.log.2.gz'
root@F005-4A88 /root [#]
</pre>

~~~
rm -v /usr/data/printer_data/logs/*.log.*
~~~
<pre>
root@F005-4A88 /root [#] rm -v /usr/data/printer_data/logs/*.log.*
removed '/usr/data/printer_data/logs/klippy.log.2020-03-01'
removed '/usr/data/printer_data/logs/klippy.log.2024-02-02'
removed '/usr/data/printer_data/logs/klippy.log.2024-02-03'
removed '/usr/data/printer_data/logs/moonraker.log.2024-02-02'
root@F005-4A88 /root [#] 
</pre>

---

~~~
cd /usr/data/moonraker/moonraker
git fetch
~~~
<pre>
root@F005-4A88 /usr/data/moonraker/moonraker [#] git fetch
remote: Enumerating objects: 1502, done.
remote: Counting objects: 100% (1152/1152), done.
remote: Compressing objects: 100% (284/284), done.
remote: Total 1502 (delta 939), reused 1049 (delta 866), pack-reused 350
Receiving objects: 100% (1502/1502), 1.07 MiB | 1.39 MiB/s, done.
Resolving deltas: 100% (1109/1109), completed with 38 local objects.
From https://github.com/Arksine/moonraker
 * [new branch]      dev-history-custom-fields-20112023 -> origin/dev-history-custom-fields-20112023
 * [new branch]      dev-machine-peripherials-20231225 -> origin/dev-machine-peripherials-20231225
   aa0f89c..61ea860  master     -> origin/master
root@F005-4A88 /usr/data/moonraker/moonraker [#] git status
HEAD detached at dde9bcc
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   moonraker/components/dbus_manager.py
	modified:   moonraker/components/file_manager/file_manager.py
	modified:   moonraker/components/file_manager/metadata.py
	modified:   moonraker/components/machine.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.files-list.before
	moonraker.conf

no changes added to commit (use "git add" and/or "git commit -a")
root@F005-4A88 /usr/data/moonraker/moonraker [#]
</pre>


~~~
cd /usr/data/moonraker/moonraker

~~~
<pre>
root@F005-4A88 /usr/data/moonraker/moonraker [#] ls -la
total 1004
drwxr-xr-x    8 1014     1014          4096 Jan 11 12:26 ./
drwxrwxr-x    4 1014     1014          4096 Jan 11 12:26 ../
-rw-r--r--    1 1014     1014           223 Aug 23 18:03 .editorconfig
-rw-r--r--    1 1014     1014        921501 Aug 23 18:03 .files-list.before
drwxr-xr-x    7 1014     1014          4096 Feb  1 00:59 .git/
-rw-r--r--    1 1014     1014            66 Aug 23 18:03 .gitattributes
drwxr-xr-x    4 1014     1014          4096 Jan 11 12:26 .github/
-rw-r--r--    1 1014     1014           114 Aug 23 18:03 .gitignore
-rw-r--r--    1 1014     1014           154 Aug 23 18:03 .readthedocs.yaml
-rw-r--r--    1 1014     1014         35129 Aug 23 18:03 LICENSE
-rw-r--r--    1 1014     1014          1980 Aug 23 18:03 README.md
drwxr-xr-x    2 1014     1014          4096 Jan 11 12:26 docs/
-rw-r--r--    1 1014     1014           713 Aug 23 18:03 mkdocs.yml
drwxr-xr-x    5 1014     1014          4096 Jan 11 12:26 moonraker/
-rw-rw-r--    1 1014     1014           741 Aug 23 18:03 moonraker.conf
-rw-r--r--    1 1014     1014           247 Aug 23 18:03 pytest.ini
drwxr-xr-x    2 1014     1014          4096 Jan 11 12:26 scripts/
drwxr-xr-x    5 1014     1014          4096 Jan 11 12:26 tests/
root@F005-4A88 /usr/data/moonraker/moonraker [#] 
</pre>

~~~
rm -v /usr/data/moonraker/moonraker/.files-list.before
~~~
<pre>

</pre>

~~~
cd /usr/data/moonraker/moonraker
git config color.ui false
git diff
git config color.ui auto
~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

---

~~~

~~~
<pre>

</pre>

---

