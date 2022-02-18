---
title: UD 4. Administració dels sistemes operatius, usuaris i grups
titlepage: true
subtitle: [\quad \quad SOM]
#author: [\quad \quad \quad \quad \quad \quad ]
lang: ca
toc-own-page: true
toc-title: Continguts
titlepage-rule-height: 0
titlepage-text-color: "262F7E"
titlepage-background: Portades.png
header-left:  UD 4. Administració dels sistemes operatius, usuaris i grups
header-right: Curs 2021-2022
footer-left: IES Jaume II el Just - SOM
footer-right: \thepage
header-includes:

- \usepackage{graphicx}
- \usepackage{draftwatermark}
- \SetWatermarkText{\includegraphics{img/logo50water.png}}
- \SetWatermarkAngle{20}
---


**Administració dels sistemes operatius, usuaris i grups**
=======================================

# Arrancada i parada del sistema. Sessions. 
De forma genèrica, solem anomenar usuari a qualsevol persona que utilitza un ordinador. Per facilitar l'administració de l'equip, el seu administrador ha de crear un compte d'usuari per a cada usuari que l'utilitzi. En fer-ho, cobrirem diversos objectius diferents: Sempre estarà identificada la persona que ha fet servir l'ordinador en cada moment. De fet, n'hi haurà prou amb consultar els logs del sistema per esbrinar quin compte d'usuari es trobava activa en un moment concret. Si cada compte és usada per un únic usuari, també tindrem identificat a l'usuari. Podrem limitar les accions que pot dur a terme cada compte d'usuari (fer servir la impressora, connectar-se a Internet, etc.). Així, aconseguirem que uns usuaris tinguin permisos per fer certes tasques i altres no, augmentant el nivell de seguretat de la instal·lació. En els sistemes operatius actuals, cada compte d'usuari està associada a un perfil. Això significa que cada usuari tindrà el seu propi fons d'escriptori, favorits d'Internet, una imatge personal per identificar la seva compte, resolució de pantalla, documents personals, la seva pròpia col·lecció d'imatges, música, vídeos, etc.

## Inici/tancament de sessió:
Quan conclou la càrrega, la majoria dels sistemes operatius moderns, mostren una pantalla d'autenticació. En ella podem triar el compte d'usuari amb la qual treballarem i, a continuació, escriure la contrasenya corresponent. Com és d'esperar, cada usuari només ha de conèixer la seva pròpia contrasenya. Un cop l'hàgim escrit, podrem començar a treballar amb el sistema operatiu.
independentment que vulguem apagar l'equip o reiniciar-lo, començarem fent clic sobre el menú del sistema a la part superior dreta de la pantalla.
En fer-ho, apareixerà un menú emergent amb diferents opcions.
Apagar l'equip des comandaments pot ser tan senzill com executar una ordre, és clar que després de prémer intro es tancarà tot el que estiguis fent i ho apagarà immediatament:

* shutdown -h now
* init 0
* halt -p
* poweroff

Si la nostra intenció és programar l'apagat tenim aquesta entrada on potser el més interessant serien els següents dos comandaments:

* shutdown -h hours: minutes & → Apagat planificat de sistema
* shutdown -c → Cancel a una aturada planificada de sistema

En certs moments també pot resultar interessant reiniciar l'ordinador mitjançant ordres, com no podia faltar també disposem de diverses opcions en linux per aconseguir aquest objectiu.

* shutdown -r now
* reboot
* init 6

També podem programar el reinici, reiniciar en un temps programat:

* shutdown -r + 10 -> reiniciarà en 10 minuts
* shutdown -r 14:30 -> reiniciarà l'equip a les 14 i mitja

La sessió d'un usuari també pot ser acabada sense necessitat d'apagar o reiniciar podent provocar pèrdues de dades en altres usuaris si estiguessin amb la seva sessió encara activa realitzant qualsevol operació.

També pot ser útil a l'hora de canviar manualment d'usuaris en una terminal ja sigui administrant, fent proves, usant aplicacions o el motiu que sigui.
Alguns comandaments per tancar la sessió són:

* logout → Tancar sessió
* skill nom_d'usuari → Tancar sessió
* exit → Sortir de l'intèrpret d'ordres (si només n'hi ha un, equival a tancar sessió, si des d'un intèrpret o usuari hem accedit a un altre intèrpret o loguejat amb un altre usuari ens tancarà l'últim i tornarà a l'anterior)


# Usuaris i grups
A Linux, els usuaris s’identifiquen amb un número d’usuari anomenat UID (User ID). Aquest número és diferent de qualsevol altre número d'UID o d'un altre usuari. És com el número de la targeta d’identificació. Aquest número identifica una sola persona i no es pot tornar a utilitzar per a una altra persona. A més, cada usuari hauria de pertànyer a un grup, anomenat grups primaris. A més, el mateix usuari pot pertànyer a altres grups anomenats grups secundaris:

* El grup principal, en la majoria dels casos, té el mateix nom que el vostre nom d’inici de sessió. El grup primari s'utilitza per defecte quan es creen nous fitxers (o directoris), es modifiquen fitxers o s'executen ordres.
* Grups secundaris: es tracta de grups que sou membres fora del grup principal. Vol dir que, si algun usuari pertany a un grup com a secundari, aquest usuari aplicarà el mateix (permís o accessibilitat) aplicat al grup del directori o del fitxer.
Un grup és un conjunt d’usuaris, però és possible que un grup tingui un sol usuari. De la mateixa manera que l’usuari té un número d’UID, els grups s’identifiquen mitjançant GID (Group ID). Com heu pogut endevinar, és un número diferent per a cada grup.

## Tipus d’usuaris:
Hi ha tres tipus d'usuaris diferents en el sistema Linux:

* Usuari root: també conegut com a superusuari o administrador. És l’usuari que té tots els privilegis i pot fer gairebé tot. Té accés total al sistema, i s’encarrega de l’administració, actualització i manteniment; El seu número de UID és 0.
* Usuaris del sistema: es generen quan s’instal·len els sistemes operatius o quan s’instal·la algun servei. Tot i que no tenen tots els privilegis, en tenen alguns depenent de l’usuari. No s’utilitzen per validar en una sessió, però són necessaris per executar alguns serveis o processos del sistema operatiu. El nombre d'UID és superior a 1 i inferior a 1000, excepte els usuaris nobody. L’UID d’aquest usuari és 65534, que és l’últim.
* Usuaris habituals: són usuaris normals que es connectaran al sistema i poden iniciar una sessió en el sistema operatiu. Tenen un directori de treball al directori /home. Tenen tot el permís d’aquest directori. La UID assignada a aquest tipus d’usuaris és superior o igual a 1000, tot i que és possible canviar-la. Quan s’instal·la el sistema operatiu, per defecte es crea un d’aquest tipus d’usuaris. Un usuari habitual pot d’accedir als fitxers de la seva propietat o als directoris  i fitxers en els quals algu li ha donat permissos
  
## Fitxers de configuració:
Els fitxers de configuració de l'administració del sistema són els fitxers que el sistema  llegeix o modifica quan es gestionen usuaris o grups.

* /etc/passwd: conté informació sobre l’usuari en cadascuna de les seves línies. La informació s’organitza en camps. El delimitador de cada camp és el caràcter “:”. L'estructura de cada línia és la següent informació:
  * nom d’usuari: és l’inici de sessió de l’usuari d’aquesta línia. És el primer camp.
  * contrasenya: Aquest camp és la contrasenya de l’usuari, però la solució significa que la contrasenya està xifrada al fitxer /etc/shadow.
  * UID: és el número UID de l’usuari
  * GID: és el número GID del grup principal de l’usuari. Aquest nombre és igual o superior a 0. El nombre 0 és el grup de números GID arrel.
  * Informació de l’usuari: camp que conté informació sobre l’usuari. El delimitador de la informació és “,” però és possible que el camp estigui buit. Aquest camp s’anomena GECOS.
  * Directori principal de l'usuari: és el camí absolut del directori personal de l'usuari (directori personal del home)
  * Command/Shell: és la ruta absoluta del shell d’inici de sessió que l’usuari utilitza per defecte. El més utilitzat és el shell bash, tot i que n’hi ha molts.
          
* /etc/shadow: Aquest fitxer conté les contrasenyes xifrades de cada usuari. És un fitxer molt important i sensible. Per tant, root o un altre usuari amb els mateixos privilegis poden llegir-lo. Cada vegada que algun usuari accedeix al sistema, Linux comprova la contrasenya d'aquest fitxer. Fa uns anys, es va utilitzar la contrasenya xifrada per desar-la a la paraula de pas del camp del fitxer /etc/passwd. Aquesta contrasenya es va xifrar amb l'algorisme de xifrat (Data Encryption Standard). Aquest algorisme utilitza la funció de cripta Linux. A causa de raons de seguretat, va començar a utilitzar aquest fitxer (/etc/shadow) i encriptació d'algorismes més complexos. Els algorismes més utilitzats són: DES, MD-5, SHA-256 i SHA-512, Blowfish. 
L’estructura del fitxer és:
Nom d'usuari: és el vostre nom d'inici de sessió.
  * Contrasenya: contrasenya xifrada de cada usuari.
  * Contrasenya canviada: Dies des de l’1 de gener de 1970 fins quan es va canviar per última vegada la contrasenya.
  * Mínim: el nombre mínim de dies requerits entre canvis de contrasenya, és a dir, el nombre de dies restants abans que l'usuari permeti canviar la seva contrasenya.
  * Màxim: el nombre màxim de dies que la contrasenya és vàlida (després que l'usuari sigui obligat a canviar la seva contrasenya)
  * Avís: el nombre de dies abans de caducar la contrasenya, se li advertirà a l'usuari que cal canviar la seva contrasenya
  * Inactiu: el nombre de dies posteriors a la caducitat de la contrasenya del compte desactivat.
  * Caduca: dies des de l'1 de gener de 1970, el compte està desactivat, és a dir, una data absoluta que especifica quan ja no es podrà utilitzar la sessió. Si aquest camp està buit, el compte no caduca mai.
          
* /etc/group: fitxer que conté els grups registrats al sistema. L’estructura si el fitxer és:
grup: x: GID: usuaris: 
on cada camp conté la informació següent:
  * Grup: és el nom del grup.
  * X: s'utilitza principalment al sistema Unix per desar la contrasenya del grup. Avui en dia, no s’utilitza excepte en alguns casos, com protegir alguns grups per evitar que algun usuari pugui accedir.
  * GID: és el nombre del grup.
  * Usuaris: és la llista d’usuaris amb això com a grup secundari. Es delimitarà cada usuari. Per conèixer el grup principal de cada usuari, cal que comproveu el fitxer /etc/passwd.

* /etc/gshadow: és el fitxer que es guarden les contrasenyes de grup. Tot i que les contrasenyes no s'utilitzen, és necessari tenir el fitxer.
* /etc/default/useradd: en aquest fitxer és possible trobar els valors per defecte per afegir algun usuari amb la comanda useradd.
* /etc/adduser.conf: conté els valors per defecte per tal que l’usuari s’afegeixi al sistema amb l’ordre adduser.
* /etc/deluser.conf: conté els valors per defecte quan un usuari s'esborra amb l'ordre delimitat.
* /etc/login.defs: fitxer que conté informació amb alguns valors sobre el xifrat de la contrasenya i altres paràmetres de la creació de l'usuari.
* /etc/shells: és una llista dels shells vàlids.


## Usuaris i gestió de grups:

### Comandes per canviar l’usuari o executar comandes amb privilegis d’administrador:
Durant la instal·lació de Linux (distribucions Ubuntu o Mint), es crea un usuari, aquest usuari no és root, però es troba a la llista anomenada   sudoers  . En aquesta llista és possible donar privilegis a usuaris habituals, i l’usuari creat durant la instal·lació n’és un. D’aquesta manera és possible executar alguna instrucció com si l’executara root.
D’altra banda, el compte root està desactivat, és a dir, no és possible iniciar la sessió com a root, tret que l’usuari tingui una contrasenya a l’arrel de root amb privilegis.
Per tant, per executar ordres amb privilegis, és obligatori utilitzar la comanda sudo abans de la comanda.

Exemple: Anem a canvair la contrasenya de root per activar-lo.
D’aquesta manera l’ordre de contrasenya (ordre per canviar la contrasenya) s’executa de forma superusuari per part de l’usuari connectat al sistema. Es suposa que l'usuari que ha iniciat la sessió es troba a la llista de sudoers ( sino fos així no podria executar la comanda).
```
  ubuntu@ubuntuSOM:~$ sudo passwd root
  [sudo] contraseña para ubuntu: 
  Introduzca la nueva contraseña de UNIX: 
  Vuelva a escribir la nueva contraseña de UNIX: 
  passwd: contraseña actualizada correctamente
```

D’altra banda, l’ordre per canviar l’usuari és su. El comandament su és una sigla d’Usuari Switch. Tenim dues opcions:

  * Sense paràmetres: en aquest cas, intenta iniciar la sessió com a root. Funciona fins i tot si el compte root està desactivat.
  * Amb paràmetre: té un paràmetre que és el nom d'usuari al qual voleu iniciar la sessió.

Si executeu la comanda com a root, us registrarà automàticament com a usuari. Si ets un usuari normal, et demana la contrasenya de l’usuari.
```	
    ubuntu@ubuntuSOM:~$ su root
	Contraseña: 
	root@ubuntuSOM:/home/ubuntu# 
```

### Comandes de gestió d’usuaris i grups:

adduser ⇒ Afegir usuaris al sistema. També s'utilitza per afegir algun usuari a un grup existent.
Sintaxi:
```
     adduser [opcions] usuari
     adduser [opcions] grup d’usuaris                   
```
Opcions:

* --grupo namegroup ⇒ L'usuari es crearà amb el grup primari especificat.
* --gid num_gid ⇒ És la mateixa opció que abans, però aquesta vegada s'utilitza el número GID en lloc del grup de nom.
* --home nom del directori home ⇒ per canviar el directori inicial de l'usuari en lloc del no predeterminat. Normalment és el nom /home/nom_usuari.

useradd ⇒ que la comanda fa el mateix tot i que s'ha d'indicar la contrasenya, si no que s'utilitza un signe d'exclamació (!) I s'afegeix al fitxer /etc/shadow. Això vol dir que l’usuari està en estat bloquejat; per tant, és necessari establir una contrasenya per a aquest compte amb l'ordre passwd. I el mateix amb el directori personal; és necessari crear un directori personal. És possible crear-lo amb les opcions de comandament.

Sintaxi:
```
	useradd [opcions] usuari
```
Opcions:	

  * -c	Descripción del usuario
  * -d	Directori home (no el crea, deu existir)
  * -e	data de caducitat del compte
  * -g	Grup per defecte (no el crea, deu existir)
  * -G	Altress grups als quals pertanyerà a part del principal
  * -s	Shell que utilitzarà (/bin/bash)
  * -u	Identificador de l’usuari (ID)
  * -m	Crea el directori home asignat a l’opció -d 

Exemple:
useradd -c “Name Surname ” -g admin -d /home/user1 -m -s /bin/bash user1
Crea un usuari que pertany al grup admin, com a home tindrà /home/user1 i el shell per defecte serà /bin/bash.

deluser ⇒ per esborrar un usuari. Existeix l'ordre userdel. Tingueu en compte que no és possible esborrar un usuari connectat en aquell moment.
Sintaxi:
```
    deluser [opcions] user.
```
Opcions:

  * - -remove-home ⇒ esborra el directori personal de l’usuari (amb el comandament userdel l’opció que fa el mateix seria -r)
  * - -remove-all-files ⇒ S'eliminaran tots els fitxers  que pertanyen a l'usuari i el directori personal.
          

addgroup ⇒ que l’ordre afegeix un grup al sistema. El mateix resultat s’obtindria amb l’adduser d’ordres i l’opció  --group:
Sintaxi:
```
      addgroup [–group] [-g gid] grupo
 ```            

delgroup ⇒ Eliminar un grup. El mateix resultat s’obtindria amb el comandant deluser  -g grupo. Tingueu en compte que el grup que se suposa que se suprimeix, no hauria de ser un grup principal de cap usuari.
	
Sintaxi:
```
      delgroup grupo
```

usermod ⇒  comanda que modifica un usuari existent. 
      
Sintaxi:

```
       usermod [opcions] usuari
```

Opcions:

  * -d directori [-m] ⇒ canviar el directori personal
  * -m ⇒ desplaça el contingut de l'antic directori personal al directori nou. Es pot utilitzar només amb l'opció -d.
  * -g grup ⇒cambieu el grup principal de l’usuari.
  * -u uid ⇒ canvia el número de uid de l'usuari.
  * -l nom ⇒ canvia el nom de l’usuari.
  * -s shell ⇒ canvia el shell


groupmod ⇒ per modificar un grup existent
Sintaxi:
```
     groupmod [opcions] grup
```

Opcions:

  * -n nom directori [-m] ⇒ canviar el grup de nom.
  * -g gid ⇒cambieu el GID del grup
          
          
gpasswd ⇒ s'utilitza per afegir o eliminar un usuari a algun grup. 
Sintaxi:
```

       gpasswd [opcions] grup usuri
       gpasswd grup 
```
Opcions:

  * -a ⇒ afegir usuari al grup
  * -d ⇒ eliminar usuaris del grup.
  * -M ⇒ afegeix diversos usuaris al grup.

Id ⇒ mostra la informació de l'usuari; per exemple, UID, nom, grups als quals pertany i GID.
Sintaxi:
```
    id [opcions] [usuaris]
```

Opcions:

  * -u ⇒ - -user ⇒ només mostra el UID de l'usuari.
  * -n ⇒ - -name⇒ mostra només el nom de l'usuari en lloc dels grups UID 
          

group⇒ mostra el nom dels grups als quals pertany l'usuari.
Sintaxi:
``` 
    group[usuari]
```

finger ⇒ Mostra la informació sobre l'usuari especificat. Sense cap usuari especificat, mostra informació sobre els usuaris connectats.
Sintaxi:
```
	finger [usuari]
```

Alguns exemples:
1. Creeu un grup nou, anomenat grup nou.
   
   sudo addgroup newgroup

2. A continuació, afegiu un usuari anomenat nou usuari.
   
	sudo adduser --ingroup newgroup newuser

3. El grup primari és grup nou.
   
	id newuser

4. Comproveu el resultat.
   
	su newuser (fem login amb l’usuari nou)

	whoami

	exit

5. Creeu un altre grup anomenat grup2.
   
	sudo adduser --group group2

6. Afegiu nou usuari a aquest grup com a grup secundari
   
	sudo adduser newuser group2

7. Comproveu el resultat
   
	cat /etc/group (fem la comprovació)

	groups newuser 

	su newuser

	exit

Borrem  el que hem fet.
```
sudo deluser --remove-home newuser
sudo delgroup group2
sudo deluser --group newgroup
```

### Ordres per canviar fitxers i directoris d’usuaris i grups.
Com sabem, cada fitxer i directori té un propietari i un grup. Per tant, s'utilitzen les ordres següents per canviar el propietari o grup de directoris i fitxers.

chown ⇒ Canvia el propietari del fitxer. És possible utilitzar-lo per canviar de grup també.
Sintaxi:
```
	chown [options] [owner[:grupo]] file/s
```
Opcions:

   * -r  - -recursivament, cambia propietari i grup dels directoris i fitxers que estan dins del principal.

chgrp ⇒ canviar el propietari del grup del fitxer. 

Sintaxi:
```
    chgrp [opcions] fitxer
```
Opcions:

   * -r - -recursive ⇒ canviar el propietari del grup per un arbre de directoris.
