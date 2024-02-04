
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


