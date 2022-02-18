---
title: UD4 .Administració de sistemes operatius, Usuaris i grups.
titlepage: true
subtitle: [\quad \quad SOM]
#author: [\quad \quad \quad \quad \quad \quad ]
lang: ca
toc-own-page: true
toc-title: Continguts
titlepage-rule-height: 0
titlepage-text-color: "262F7E"
titlepage-background: Portades.png
header-left: UD4 .Administració de sistemes operatius, Usuaris i grups.
header-right: Curs 2021-2022
footer-left: IES Jaume II el Just - SOM
footer-right: \thepage
header-includes:

- \usepackage{graphicx}
- \usepackage{draftwatermark}
- \SetWatermarkText{\includegraphics{img/logo50water.png}}
- \SetWatermarkAngle{20}
---


**Usuaris, grups i permisos**
=======================================

**Usuaris, grups i modificacions**

* Crea un grup anomenat 'equip' deixant que el SO estableixi el GID.

* Crea l'usuari 'juanito' establint que la seva UID siga 1045.

* Crea el usari 'pepito' amb UID 1046 i amb grup primari 'equip'.

* Modifica el nom de el grup 'equip' perquè passi a dir-se 'equipas'.

* Afegeix a 'juanito' com usario de 'equipas' (en aquest cas no serà el seu grup primari).

* Mostra la informació de 'pepito’ que apareix en el fitxer /etc/passwd

* Amb el comandament 'id' mostra la información de 'pepito' i després la de 'juanito'.

* Mostra els grups als quals pertany 'juanito'. 
  
* Ara mostra els grups de 'pepito'.

* Esborra els usuaris creats i finalment esborra el grup 'equipas'.

* Mostreu el nom dels propietaris i dels grups dels arxius /etc/hosts i ~/.bashrc, usant ls.
  * {instrucció, una sola)}
  * {indiqueu els noms dels propietaris/grups}

* Mostreu nom, grup, identificador de nom i de grup vostre com a usuari (comanda id)
  * {instrucció i sortida per pantalla} 

* Executeu la instrucció exit
  * {expliqueu el que ha passat en executar-la}

* Mostreu propietari i grup en forma numèrica dels arxius /etc/hosts i ~/.bashrc usant ls.
  * {instrucció, una sola }
  * {indiqueu els identificadors de propietaris/grups}

* El nou propietari de l'arxiu ~/.bashrc ha de passar a ser el root (comanda chown). 
  * {instrucció}
  * {resultat per pantalla}

* El nou grup de l'arxiu ~/protocols.copia ha de ser users (comanda chgrp).
  * {instrucció}









**Permisos**

* Creeu un arxiu anomenat protocols.copia i un directori anomenat pp al teu home. Mostreu els permisos sobre l'arxiu ~/protocols.copia i sobre el directori ~/pp (comanda ls i opcions).
* Copieu l'arxiu ~/protocols.copia dins el directori ~/pp.
* Traieu-vos el dret d'escriptura sobre el directori ~/pp mitjançant la comanda chmod i demostreu que realment no hi podeu escriure (copiar algun arxiu, crear subdirectoris,....)
  * {instrucció,  visualització dels nous drets i demostració de la impossibilitat d'escriure a pp}
* Demostreu que malgrat no podeu escriure a ~/pp, sí que podeu entrar-hi.
* Torneu al vostre directori casa (sortiu del directori ~/pp) i traieu-vos el dret d'execució sobre  el directori ~/pp. Demostreu que ara no hi podeu accedir (cd, ls -l).
  * {instrucció, visualització dels nous drets, prova de les comandes cd pp, ls -l pp,}.
* Malgrat no podeu entrar a ~/pp, sí que podeu veure'n el contingut amb ls pp 
  * {explicació del fet}
* Deixeu el directori ~/pp amb els drets --xr-xr-x. Demostreu que malgrat no poder llistar el directori pp, sí que podem entrar-hi i mostrar el contingut de l'arxiu que conté.
  * {instrucció,  visualització dels nous drets,demostració de les comandes, i explicació}
* Deixeu el directori ~/pp amb els drets originals rwxr-xr-x. Heu de fer-ho usant chmod amb paràmetre numèric en octal.
* Deixeu l'arxiu ~/pp/protocols.copia amb els drets rwx---r-x. Heu de fer-ho usant chmod amb paràmetre numèric en octal.

