

pour que le serveur web serve le fichier `/usr/data/creality/userdata/history/print_history_record.json` via `http://<ip>/downloads/humbnail/historyL.txt`

Creation d'un service pour faire un lien symbolique du fichier que l'on veux rendre dispo par le serveur web pré-installé

Bien noter que ici, le lien symbolique doit etre fait apré le lancement du service `/etc/init.d/S99start_app`, qui lance l'application qui générer et maintient a jour le fichier `/usr/data/creality/userdata/history/print_history_record.json`  
D'où le nom `S99t_hist_http` alphabétiquement aprés `S99start_app` )

~~~
cat > /etc/init.d/S99t_hist_http<<'===EOF==='
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

Bien noter que le fait, au début, de mettre entre quote la ligne qui permet d'identifier la fin du bloc, evite l'interprétation des caractères spéciaux, et variables. Attention forcement il ne faut pas que le corps du bloc contienne une ligne identique a celle utilisé pour identifier la fin du bloc (ici mise entre quote au début). cf [https://stackoverflow.com/questions/6896025/echo-a-large-chunk-of-text-to-a-file-using-bash](https://stackoverflow.com/questions/6896025/echo-a-large-chunk-of-text-to-a-file-using-bash).

rendre executable le fichier créé
~~~
chmod a+x /etc/init.d/S99t_hist_http
~~~

et enfin 

executer le service 
~~~
/etc/init.d/S99t_hist_http start
~~~

ou relancer/rebooter le système
~~~
reboot
~~~

(Normalement là, a chaque démarrage, le lien symbolique sera créé par se service. Et donc on retrouve a l'url `http://<ip>/downloads/humbnail/historyL.txt` le contenu de `/usr/data/creality/userdata/history/print_history_record.json` )

Chez moi c'est l'adresse [http://192.168.1.23/downloads/humbnail/historyL.txt](http://192.168.1.23/downloads/humbnail/historyL.txt)










