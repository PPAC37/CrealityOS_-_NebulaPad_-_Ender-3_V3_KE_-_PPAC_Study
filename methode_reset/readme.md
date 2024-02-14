# Méthode de reset

La méthode de reset des K1* https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Reset-Factory-Settings semble fonctionner pour les Ender-3 V3 KE.

(

Dommage il semble que l'on doit absolutment avoir la page.html en local pour que cela fonctionne ...


Je me suis permis de mettre la page de reset `Creality_K1_Reset_Utility.html` de Gilouz en ligne via ghithub.io a l'adresse

https://ppac37.github.io/CrealityOS_-_NebulaPad_-_Ender-3_V3_KE_-_PPAC_Study/methode_reset/Creality_K1_Reset_Utility.html

Pour ne pas avoir a telecharger le [Creality_K1_Reset_Utility.zip](https://github.com/Guilouz/Creality-K1-and-K1-Max/raw/main/Scripts/Creality_K1_Reset_Utility.zip), le décompresser, pour obtenir le `Creality_K1_Reset_Utility.html` qui permet le reset (un script js embarqué envoie un `{"method":"set","params":{"resetSystem":15}}` au web socket port 9999 de l'imprimante).

Un grand merci à https://github.com/Guilouz

)

---

https://discord.com/channels/1154500511777693819/1186800299424366643/1207072102369202186

~~~
echo "all" | nc -U /var/run/wipe.sock
~~~

---

https://discord.com/channels/1154500511777693819/1186800299424366643/1207080347817484338

just be aware, it triggers a reboot automatically and deletes EVERYTHING

if you want to do the equivalent of the factory reset that is initiated from the k1 screen you can use this command:

~~~
echo "part" | nc -U /var/run/wipe.sock
~~~

I have posted above what each of them actually does in terms of deletions

---

https://discord.com/channels/1154500511777693819/1186800299424366643/1207203706500550676

~~~
echo "part" | nc -U /var/run/wipe.sock
~~~
=
~~~
/bin/rm called with args: -rf /usr/data/wpa_supplicant.conf
/bin/rm called with args: -rf /usr/data/ai_image
/bin/rm called with args: -rf /usr/data/timelapse
/bin/rm called with args: -rf /usr/data/lost+found
/bin/rm called with args: -rf /overlay/upper/*
~~~
