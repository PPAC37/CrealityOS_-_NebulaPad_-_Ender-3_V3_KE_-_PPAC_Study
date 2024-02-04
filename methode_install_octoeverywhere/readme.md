
Pré-requis :
- Avoir un compte https://octoeverywhere.com/

Le plus simple c'est surement de passer par le "Installation Helper Script" de Guilouz [https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script
)  

~~~
cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
cd && sh ./installer.sh
~~~

---

Sinon en manuel 

~~~
cd /usr/data
git clone https://github.com/QuinnDamerell/OctoPrint-OctoEverywhere.git octoeverywhere
cd octoeverywhere
sh ./install.sh
~~~

<pre>
...
Website: https://octoeverywhere.com/code
Code:    935409
</pre>

Et si tout c'est bien passé vous devrez pouvoir vous connecter via une url de la forme https://nom_de_machine.octoeverywhere.com/#/

<!--
https://e3v3ke_ppac.octoeverywhere.com/#/
-->
