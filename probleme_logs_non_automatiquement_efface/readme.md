
---
---



~~~

~~~

<pre>
root@F005-4A88 /root [#] logrotate
-sh: logrotate: not found
root@F005-4A88 /root [#]
</pre>


---
---



~~~

~~~

<pre>
root@F005-4A88 /root [#] find / | grep logrotate
/usr/data/nginx/logrotate.d
/usr/data/nginx/logrotate.d/nginx
root@F005-4A88 /root [#]
</pre>


---
---



~~~

~~~

<pre>
root@F005-4A88 /root [#] du -hc /var/log/
0	/var/log/creality/original
56.0K	/var/log/creality/local_gcode/original
12.0K	/var/log/creality/local_gcode/humbnail
72.0K	/var/log/creality/local_gcode
80.0K	/var/log/creality
0	/var/log/nginx/scgi
0	/var/log/nginx/uwsgi
0	/var/log/nginx/fastcgi
0	/var/log/nginx/proxy
0	/var/log/nginx/client-body
0	/var/log/nginx
4.0K	/var/log/dbus
0	/var/log/subsys
232.0K	/var/log/
232.0K	total
root@F005-4A88 /root [#] 


</pre>



---
---



~~~

~~~

<pre>
root@F005-4A88 /root [#] ls -laRh /var/log/
/var/log/:
total 149K   
drwxrwxrwt    6 root     root         500 Feb  4 18:39 .
drwxr-xr-x    1 root     root        1.0K Feb  2 16:29 ..
-rw-r--r--    1 root     root          56 Mar  1  2020 .mcu_version
srwxr-xr-x    1 root     root           0 Mar  1  2020 ai_server_uds
-rw-r--r--    1 root     root           0 Mar  1  2020 bsa_server.log
drwxr-xr-x    4 root     root         120 Mar  1  2020 creality
drwxr-xr-x    2 root     root          60 Mar  1  2020 dbus
-rw-r--r--    1 root     root       59.2K Mar  1  2020 hci_snoop.log
lrwxrwxrwx    1 root     root          10 Mar  1  2020 klipper_host_mcu -> /dev/pts/0
srwxr-xr-x    1 root     root           0 Feb  4 16:59 klippy_client
srwxr-xr-x    1 root     root           0 Feb  4 16:59 klippy_uds
-rw-r--r--    1 root     root           0 Feb  4 16:59 load_done
-rw-r--r--    1 root     root         135 Mar  1  2020 mcu_update.log
-rw-r--r--    1 root     root       74.8K Feb  4 18:39 messages
drwxr-xr-x    7 root     root         240 Mar  1  2020 nginx
lrwxrwxrwx    1 root     root          10 Mar  1  2020 printer -> /dev/pts/1
-rw-r--r--    1 root     root          33 Mar  1  2020 resolv.conf
drwxr-xr-x    2 root     root          60 Mar  1  2020 subsys
srwxr-xr-x    1 root     root           0 Mar  1  2020 sys_sock
prw-r--r--    1 root     root           0 Mar  1  2020 uvc_fifo
srwxr-xr-x    1 root     root           0 Mar  1  2020 wpa_ctrl_1271-0
srwxr-xr-x    1 root     root           0 Mar  1  2020 wpa_ctrl_1271-1
srwxr-xr-x    1 root     root           0 Mar  1  2020 wpa_ctrl_1271-2
srwxr-xr-x    1 root     root           0 Feb  4 16:59 wpa_ctrl_1952-0
srwxr-xr-x    1 root     root           0 Feb  4 16:59 wpa_ctrl_1956-0

/var/log/creality:
total 8K     
drwxr-xr-x    4 root     root         120 Mar  1  2020 .
drwxrwxrwt    6 root     root         500 Feb  4 18:39 ..
-rw-r--r--    1 root     root         335 Mar  1  2020 bind_qrcode.png
drwxr-xr-x    4 root     root         100 Feb  4 16:59 local_gcode
drwxr-xr-x    2 root     root          40 Mar  1  2020 original
-rw-r--r--    1 root     root         567 Mar  1  2020 user_service_qrcode.png

/var/log/creality/local_gcode:
total 4K     
drwxr-xr-x    4 root     root         100 Feb  4 16:59 .
drwxr-xr-x    4 root     root         120 Mar  1  2020 ..
drwxr-xr-x    2 root     root          80 Feb  4 16:59 humbnail
-rw-r--r--    1 root     root         796 Feb  4 16:59 local_gcode_file_info.json
drwxr-xr-x    2 root     root          60 Feb  4 16:59 original

/var/log/creality/local_gcode/humbnail:
total 12K    
drwxr-xr-x    2 root     root          80 Feb  4 16:59 .
drwxr-xr-x    4 root     root         100 Feb  4 16:59 ..
lrwxrwxrwx    1 root     root          61 Mar  1  2020 historyL.txt -> /usr/data/creality/userdata/history/print_history_record.json
-rwxr-xr-x    1 root     root        8.7K Feb  4 16:59 kb_cabeza para lengua-Ender-3 V3 KE_0.4_CR-PLA 215_1h5m.png

/var/log/creality/local_gcode/original:
total 56K    
drwxr-xr-x    2 root     root          60 Feb  4 16:59 .
drwxr-xr-x    4 root     root         100 Feb  4 16:59 ..
-rwxr-xr-x    1 root     root       55.5K Feb  4 16:59 kb_cabeza para lengua-Ender-3 V3 KE_0.4_CR-PLA 215_1h5m.png

/var/log/creality/original:
total 0      
drwxr-xr-x    2 root     root          40 Mar  1  2020 .
drwxr-xr-x    4 root     root         120 Mar  1  2020 ..

/var/log/dbus:
total 4K     
drwxr-xr-x    2 root     root          60 Mar  1  2020 .
drwxrwxrwt    6 root     root         500 Feb  4 18:39 ..
-rw-r--r--    1 root     root          33 Mar  1  2020 machine-id

/var/log/nginx:
total 0      
drwxr-xr-x    7 root     root         240 Mar  1  2020 .
drwxrwxrwt    6 root     root         500 Feb  4 18:39 ..
drwx------    2 www-data root          40 Mar  1  2020 client-body
-rw-r--r--    1 root     root           0 Mar  1  2020 error.log
drwx------    2 www-data root          40 Mar  1  2020 fastcgi
-rw-r--r--    1 root     root           0 Mar  1  2020 fluidd-access.log
-rw-r--r--    1 root     root           0 Mar  1  2020 fluidd-error.log
-rw-r--r--    1 root     root           0 Mar  1  2020 mainsail-access.log
-rw-r--r--    1 root     root           0 Mar  1  2020 mainsail-error.log
drwx------    2 www-data root          40 Mar  1  2020 proxy
drwx------    2 www-data root          40 Mar  1  2020 scgi
drwx------    2 www-data root          40 Mar  1  2020 uwsgi

/var/log/nginx/client-body:
total 0      
drwx------    2 www-data root          40 Mar  1  2020 .
drwxr-xr-x    7 root     root         240 Mar  1  2020 ..

/var/log/nginx/fastcgi:
total 0      
drwx------    2 www-data root          40 Mar  1  2020 .
drwxr-xr-x    7 root     root         240 Mar  1  2020 ..

/var/log/nginx/proxy:
total 0      
drwx------    2 www-data root          40 Mar  1  2020 .
drwxr-xr-x    7 root     root         240 Mar  1  2020 ..

/var/log/nginx/scgi:
total 0      
drwx------    2 www-data root          40 Mar  1  2020 .
drwxr-xr-x    7 root     root         240 Mar  1  2020 ..

/var/log/nginx/uwsgi:
total 0      
drwx------    2 www-data root          40 Mar  1  2020 .
drwxr-xr-x    7 root     root         240 Mar  1  2020 ..

/var/log/subsys:
total 0      
drwxr-xr-x    2 root     root          60 Mar  1  2020 .
drwxrwxrwt    6 root     root         500 Feb  4 18:39 ..
-rw-r--r--    1 root     root           0 Mar  1  2020 dbus-daemon
root@F005-4A88 /root [#] 


</pre>



---
---


/etc/init.d/S99start_app 
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

<pre>

</pre>



---
---



~~~
ll /usr/data/creality/userdata/log
~~~

<pre>
root@F005-4A88 /root [#] ll /usr/data/creality/userdata/log
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



---
---



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
}root@F005-4A88 /root [#] 
</pre>



---
---



~~~

~~~

<pre>

</pre>


