---
title: UD 5. Administració dels sistemes operatius. Gestió de processos
titlepage: true
subtitle: [\quad \quad SOM]
#author: [\quad \quad \quad \quad \quad \quad ]
lang: ca
toc-own-page: true
toc-title: Continguts
titlepage-rule-height: 0
titlepage-text-color: "262F7E"
titlepage-background: Portades.png
header-left:  UD 5. Administració dels sistemes operatius. Gestió de processos
header-right: Curs 2021-2022
footer-left: IES Jaume II el Just - SOM
footer-right: \thepage
header-includes:

- \usepackage{graphicx}
- \usepackage{draftwatermark}
- \SetWatermarkText{\includegraphics{img/logo50water.png}}
- \SetWatermarkAngle{20}
---


**Administració dels sistemes operatius**
=======================================

# Gestió de processos.

## Definició de procés:
Se sap que un procés és un programa que utilitza la CPU o bé es carrega principalment a la memòria. La diferència entre  procés i programes és que, cada vegada que executem un programa  es crea un procés nou i diferent. A més, podem tenir diferents processos del mateix programa  al mateix temps i el context de cada procés és diferent.
Els processos funcionen de la mateixa manera que els usuaris i els grups, tenen assignat  un nombre.
Aquest número es diu Process ID (PID), identifica cada procés i és diferent per a cada procés.

## Gestió de processos:
Per gestionar processos es poden utilitzar les ordres següents:

* ps ⇒ informa sobre l’estat del procés. Disposa de diferents opcions per mostrar columnes diferents. Les columnes més destacades són:
  * USUARI ⇒ usuari amb qui s’executa el procés
  * PID ⇒ Identificador del procés 
  * PPID ⇒ Identificadors del procés pare
  * UID ⇒Identificador del propietari del procés
  * TTY ⇒ informació sobre quin terminal està executant el procés.
  * TIME t⇒ temps acumulat de la CPU
  * CMD ⇒ nom del programa que inicia el procés
  * RSS⇒ (mida del conjunt de residents) Mida de la part resident del procés. És la quantitat de la memòria principal que ha utilitzat el procés (KiB)
  * NI ⇒ prioritat del procés.
  * % CPU⇒ percentatge de la CPU utilitzada
  * STAT⇒Estat del procés. Els estats del procés poden ser:
    * R ⇒ procés en curs o en cua llesta
    * S ⇒ Bloquejat (a l'espera que tinguin lloc altres esdeveniments dins del procés.)
    * T ⇒ aturat.
    * D ⇒ esperant altres esdeveniments, alguna tasca d'entrada / sortida
    * Z ⇒ zombi, procés acabat, però ha d’informar al procés pare.


Sintaxi:

		ps [opcions]

Opcions:

* -A ⇒ mostra les columnes d'informació: PID, TTY, TIME, CMD
* -e ⇒ mostra informació sobre tot el procés del sistema (el mateix que -A)
* -l ⇒ mostra molta informació sobre els processos (el resultat és diferent segons el signe - abans de l’opció)
* -u pepe  mostra la informació de l'usuari pepe.
* -ely ⇒ que les opcions s’utilitzen juntes per tal de mostrar tota la informació com a PID,PPID, HORA, CMD, NI, RSS ,. . .
* aux ⇒ (sense signe -) mostra les columnes de USER, PID, RSS, TTY, STAT,TEMPS,...



        pstree ⇒ mostra els processos en execució com a arbre.

Sintaxi:

        pstree [opcions]

Opcions:

* -u ⇒ mostra el propietari del procés

Exemples:

1. Mostra la informació de tots els processos que s'estan executant.
2. Mostra el PID d'alguns processos d'execució.
3. Mostra tots els processos com a arbre i mostra els propietaris. Pagina  la sortida

Solució:

1. ps -aux
2. ps -A | nom_proc grep -i
3. pstree -Gu | more


        nohup, & ⇒ S'utilitza per executar processos en segon pla. En qualsevol cas, es troba la terminal disponible per executar ordres mentre el procés en segon pla s’està executant.

Sintaxi:
```
        nohup ordre &

```
```

        sleep ⇒ aquest comandament s'utilitza per retardar un període de temps determinat. La unitat per defecte està en segons, però és possible utilitzar-lo amb minuts, hores i dies parells (m, h, d).
```
Exemple:

sleep 5 ⇒ 5 segons es retardarà.

Sleep 5 m ⇒ 5 minuts de retard.

Exemples:

1. Executeu l'ordre de suspensió per temporitzar 10 segons i prova a executar una  altra comanda com ls -l. Mireu que la segona ordre no s’executarà desprès de  deu segons.
2. Executeu la comanda de suspensió per retardar-la de nou 10 segons. Però aquesta vegada utilitza la comanda per enviar-la  a segon pla (nohup o &).

Solució:

1. sleep 10
2. sleep 10 o nohup sleep 10 &

Ara, la sol·licitud està disponible per executar noves ordres i és possible executar-la ls o algun altre ordre a causa de l'ordre de suspensió s'està executant en segon pla.


        renice ⇒  la comanda s’utilitza per modificar la prioritat d’un procés en execució

Sintaxi:

        renice [opcions] prioritat PID_process

Opcions:

* -p ⇒ s'utilitza per si voleu aplicar la comanda a més d'un procés.
* -u ⇒ s'utilitza en cas que l'objectiu sigui aplicar la comanda a tots els processos d’algun usuari.

Exemples:

1. L'objectiu desitjat per a un usuari és executar una operació científica en un procés, però mentre que aquest procés s’executa, l’usuari vol executar un joc. Per tant, l'usuari vol canviar la prioritat del procés científic des de que s'està executant el joc. Si el procés científic està utilitzant el PID 785:

renice +15 785

on la prioritat més positiva és la prioritat inferior

2. Al ser l’administrador d’usuaris del sistema, es fa evident que s’executa un usuari molts processos. Per tant, és possible canviar tots els processos d'aquest usuari:

renice +19 -nom_usuari


     nice ⇒ Aquest comandament s’utilitza per establir la prioritat del procés. 
     
La prioritat disponible per al procés pot anar de -20 (prioritat màxima) a 19 (prioritat mínima). Es pot veure la prioritat a la columna NI (comanda ps). Més endavant, es calcula la prioritat real, i es pot veure a la columna PRI (comanda ps).

Sintaxi:
		
        nice [opcions] comanda

Opcions:

* -n número ⇒ la comanda s’executarà amb la prioritat indicada.

Exemple:

Si l'usuari vol gravar l'ISO d'Ubuntu al cd-Rom, però al mateix temps vol executar LliureOffice,  per tal d'anul·lar alguna tasca, l'usuari pot executar la comanda per realitzar el Ubuntu iso amb la prioritat establerta, ja que fer un iso és un procés molt exigent en termes de recursos utilitzats.

nice -n 19 dd if=/dev/cdrom of=~/ubuntu-19.10-desktop-amd64.iso


        jobs ⇒ mostra l'estat de les tasques iniciades a la finestra del terminal actual. Les feines ho són numerats a partir de l’1 de cada sessió. Alguns programes utilitzen els números d'identificació de treball en lloc de PIDs. Per suspendre algun procés, cal prémer les tecles CTRL + Z.

Sintaxi:
```
        jobs

```

        fg ⇒ que la comanda s’utilitza per enviar a primer pla els processos que es troben en segon pla o aturat.

Sintaxi:

        fg %n

on n és el número de la llista que apareix per la comanda Jobs. Si s'especifica algun procés, el processar amb la marca + a la llista d'ordres de treball que s'envia a primer pla.

        bg ⇒ Aquesta ordre s'utilitza per reiniciar un procés de fons aturat.

Sintaxi:

        bg %n

on n és el número de la llista que apareix per l'ordre Jobs.

        kill ⇒ per matar el procés indicat. S'utilitza per enviar alguns altres senyals al procés.

Sintaxi:

        kill [opcions] PID

Opcions:

* -9 ⇒ -SIGKILL⇒ matar el procés el PID del qual s'envia com a argument.
* -l ⇒ mostra tots els senyals que es poden enviar al procés.

        killall ⇒ matar tots els processos relacionats amb el procés indicat. Aquesta vegada, el nom de el procés s'ha d'especificar en lloc del número de procés.

Sintaxi:

        killall [opcions] nom_procés

Opcions:

* -kill ⇒ matar el procés.
* -i ⇒pregunta si realment es vol matar el procés.
* -l ⇒ mostra tots els senyals que es poden enviar al procés.

        Time ⇒ s'executa amb una ordre per saber el temps que es dedica a executar la comanda, recursos utilitzats, etc.

Sintaxi:
```
        time comanda
```
```

        top⇒ Mostra informació sobre el sistema i els processos executats. La informació s’actualitza cada 3 segons.
```
Sintaxi:

        top [opcions]

Opcions:

* -d ⇒ per canviar el retard (en segons) entre les actualitzacions de la part superior.

Exemples:

1. Executeu nano text4.txt.
2. Atureu-lo i envieu-lo a  segon pla.
3. Comproveu-ho.
4. Executeu nano text5.txt en segon pla.
5. Envieu el primer procés a primer pla. Això vol dir que el procés es torna a executar.
6. Tanca nano
7. Mata el segon procés.

Solució:

1. nano txet4.txt
2. CTRL + Z
3. jobs
4. nano text5.txt &
5. jobs  / fg% 1
6. CTRL + X
7. kill % 2


Exemples finals:

1. Instala 'leafpad' 
```
sudo apt-get install leafpad 
```
2. Executa 'leafpad' de manera que vaja directament a segon plà. Ara mostra els treballs en execució o segon pla.Porta a primer pla de nou el procés  'Leafpad'. Amb la combinació de tecles corresponent, envia a segon pla  aquest procés. Torna a mirar els treballs oberts. Mata el procés corresponent a 'Leafpad'. Torna a mirar els treballs oberts.
Com veus, tot i que abans ja s'havia matat el procés, seguia apareixent a la llista perquè es pugui veure que ja no va a aparèixer més. Després tancar-lo amb normalitat apareix el procés amb l'estat Fet. Després de tancar-lo amb el senyal SIGTERM apareix el procés amb l'estat Acabat. La segona vegada que l'executem desapareixen els processos.
```
leafpad & 
jobs
fg %1 
CONTROL Z 
jobs 
kill %1  o bien killall –KILL leafpad o kill -9 PID 
jobs 
jobs 
```

3. Executa de nou 'Leafpad' perquè vagi a segon pla. Executa 'gedit' perquè vagi també a segon pla. Revisa els treballs oberts. Envia a primer pla a 'gedit'. Després tanca-ho des de l'entorn gràfic. Revisa els treballs oberts i mira si hi ha diferent informació entre matar el procés amb kill o des de l'entorn gràfic. Torna a executar 'gedit' perquè vagi a segon pla. Ara envia a primer pla a 'Leafpad'. Amb la combinació de tecles corresponent envia-ho a segon pla. Llista els treballs oberts. Mata els processos de 'gedit' i de 'Leafpad'. Mostra les tasques oberts
```
leafpad & 
gedit & 
jobs
fg %2 jobs 
gedit &
fg leafpad 
CONTROL Z 
jobs
kill %1 %2 
jobs
```

# Instalacions i actualitzacions

## El software

\begin{figure}
\centering
\includegraphics[width=11cm]{img/software.png}
\caption{El software}
\end{figure}

### Què són les dependències?

Un Programari normalment no funciona si no té una sèrie de llibreries o programes de suport que el propi programari fa servir per no haver d'implementar ell mateix totes les funcions, llibreries de dibuixat, d'accés a base de dades ...
Important: És tasca dels programadors del Programari indicar quines són les dependències de la mateixa, però a l'igual que hi ha errors en el codi, de vegades ocorren errors en la definició de les dependències i serà tasca dels administradors de sistemes fer que el Programari funcioni en els sistemes.
Les dependències solen estar especificades en fitxers Readme.txt, en les instruccions d'instal·lació o en el cas dels compilats i preparats per a la seva distribució aquestes dependències poden ser consultades via els gestors de paquets, tal com veurem més endavant en el tema.
Si una dependència no està instal·lada, el programari pot no funcionar o senzillament no funcionar en absolut. És totalment indispensable que les dependències estiguin instal·lades, a l'acció d'instal·lar les dependències i les dependències de les mateixes en cert ordre se li crida Resolució de dependències.

### La versió d'un Programari (versionat)
El versionat de programari és el procés d'assignació d'un nom, codi o número únic, a un programari per a indicar el seu nivell de desenvolupament. Generalment s'assigna dos nombres, mayor.menor (en anglès: major.minor), que van incrementant a mesura que el desenvolupament de programari augmenti i es requereixi l'assignació d'un nou nom, codi o número únic. Encara que menys habituals, també pot indicar un altre nombre més, micro, i la fase de desenvolupament en què es troba el programari.
S'augmenta el nombre quan:

* major: el programari pateix grans canvis i millores.
* menor: el programari pateix petits canvis i / o correccions d'errors.
* micro: s'aplica una correcció al programari, i al seu torn pateix pocs canvis.
* fase: s'indica si es troba en una fase de desenvolupament que no sigui la final o estable, és a dir, una fase inestable o en proves. Se sol indicar amb un guió seguit de la fase corresponent en minúscules, o un espai seguit de la fase. Hi pot haver diverses versions d'una mateixa fase, per indicar l'avanç en el desenvolupament de programari però mantenint la fase per indicar que encara és inestable, indicant afegint un nombre a la fi de el nom de la fase que va incrementant conforme es publiquin noves versions d'aquesta fase.
  
  
### Seguretat i actualitzacions
Les versions de programari són sempre "creixents" en el temps, i és tasca dels administradors de sistemes mantenir el programari instal·lat actualitzat i operatiu. Això és especialment important en servidors i estacions de treball crítiques, ja que un programari desactualitzat, és un programari vulnerable. Els virus, hackers, i en general aquell programari que tracta d'aprofitar-se de fallades de programari es recolzen en "errors coneguts" de l'programari que es troba instal·lat per poder aconseguir els seus objectius. A continuació es mostra un gràfic (2014) que mostra els errors detectats en el dia "0" del llançament de cada paquet de programari i els bugs que encara persisteixen en l'any següent. Ens adonem de seguida que si no actualitzem el programari, tots els errors que hi poden ser utilitzats pels atacants per a comprometre la seguretat.

### Paquets en linux:
Els paquets existents en GNU / Linux, són dependents de la distribució en la qual s'estiguin fent servir; són utilitzats normalment per a la compressió d'aplicacions en diferents formats per a diferents mitjans d'instal·lació. Aquests són un conjunt de fitxers que contenen instruccions per a la reconstrucció de l'aplicació dins del sistema nou, dins d'aquests, podem trobar, Paquets Binaris i Paquets de codi Font.
Els Paquets Binaris, contenen, com s'esmenta, la informació necessària per reconstruir una aplicació en un sistema nou, sense necessitat de trobar-se en la mateixa computadora; els més comuns són:

* DEB: Contenen executables, arxius de configuració, pàgines d'informació, drets de copyright i altres documentacions, els paquets Debian es col·loquen en arxius .deb. El nom del paquet ha de contenir:
  
         <NumeroDeVersión> - <VersiónDeDebian> - <ArquitecturaDeDebian> .deb

Un desavantatge d'aquest tipus de paquets, és el seu sistema d'actualització, a causa que, es necessita tenir tots els arxius, com si es tractés una nova instal·lació. Aquests paquets també són usats per distribucions basades en la distribució Debian, algunes d'aquestes, són: Ubuntu, Kubuntu, ZorinOS, Linux Mint, entre otras.

* RPM: Per les seves sigles en anglès Redhat Package Manager, aquest tipus d'empaquetat per Linux va ser desenvolupat per a la distribució de Red Hat, per tal de crear un sistema fàcil de crear i instal·lar. Actualment totes les distribucions basades en Red Hat ocupen els paquets RPM, algunes d'elles són: Fedora i openSUSE. Un avantatge, sobre aquest tipus de paquets sobre altres, és la seva forma d'actualització per a les aplicacions, aquests, no necessiten tenir les mateixes dades que l'instal·lador original, només pot incloure (si es desitja) els arxius que s'actualitzaran, això redueix altament el pes del paquet.
* TGZ: És un arxiu de paquets específic per a Unix, comprimit amb el compressor GNU Zip. És un paquet de codi font, ocupat per contenir aplicacions, i el seu codi font, per no haver de crear un tipus de paquet específic per a cada distribució. A diferència dels paquets .deb, o .rpm, aquest no conté instruccions particulars d'instal·lació per a cada distribució, de manera que la instal·lació del contingut haurà de ser compilat per l'usuari.
* Ebuild: Paquet usat només per la distribució Gentoo, consisteix en un script bash, executable només en un entorn específic. Els seus arxius, deuen ser arxius de text amb l'extensió .ebuild. El nomenament d'aquest paquet ha d'obeir la regla següent:
  
        nom-versión.ebuild

El contingut del nom només pot contenir lletres minúscules sense accentuar, dígits del zero al nou, guions, guions baixos o el signe d'addició.

## Les actualitzacions
Les actualitzacions dels paquets poden realitzar-se amb tan sols una ordre: 

        apt-get upgrade 

Podem utilitzar aquesta opció per actualitzar els paquets de la distribució actual, o bé per actualitzar a una nova distribució, tot i que el comandament és una millor opció.

        apt-get dist-upgrade

És molt útil utilitat junt amb l'opció -u. Aquesta opció mostra la llista completa de paquets que APT s'actualitzarà. Sense ella, s'estaria actualitzant a cegues. APT descarregarà les versions més recents de cada paquet i les instal·larà de la manera més apropiada. És molt important executar apt-get update abans de provar això.

\begin{figure}
\centering
\includegraphics[width=11cm]{img/update.png}
\caption{actualización}
\end{figure}


## Els repositoris

Podem veure la llista de repositoris principal d'Ubuntu escrivint

        sudo nano /etc/apt/sources.list


\begin{figure}
\centering
\includegraphics[width=11cm]{img/repositoris.png}
\caption{Els repositoris }
\end{figure}

El primer que hem de fer és una còpia per evitar-nos problemes davant de qualsevol modificació.
Exemples:

        deb-src http://archive.ubuntu.com/ubuntu groovy universe restricted main multiverse

on:

* deb: Indica un repositori de paquets prèviament compilats.
* deb-src: És un repositori de codi font de programes.
* http://archive.ubuntu.com/ubuntu: És l'identificador uniforme de recursos (per les seves sigles en anglès). És el link d'accés al servidor on està el repositori.
* groovy: Indica la versió de sistema operatiu.
* universe restricted main multiverse: indica el tipus de repositori.

Perquè qualsevol canvi que fem en els repositoris funcioni, hem de guardar la llista primer i desprès  actualitzar la llista de repositoris.
També podem afegir repositoris des de la línia de comandes:

        sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ groovy main'
        sudo apt update

La comanda sudo add-apt-repository també s'utilitza per als paquets personals d'arxius. Per exemple per afegir el repositori ppa de Krita, escrivim:

        sudo add-apt-repository ppa: kritalime/ppa
        sudo apt update


## Instalar paquets des de els repositoris

### Comanda apt:

Per instal·lar un paquet nou:

        $ sudo apt-get install nom_del_paquet

Opció remove  per eliminar un paquet del nostre sistema utilitzem:

        $ sudo apt-get remove nom_del_paquet


\begin{figure}
\centering
\includegraphics[width=11cm]{img/apt.png}
\caption{La comanda apt }
\end{figure}

### Comanda dpkg


\begin{figure}
\centering
\includegraphics[width=11cm]{img/dpkg.png}
\caption{La comanda dpkg }
\end{figure}


### Comanda rpm

A Red Hat l'eina per excel·lència per administrar paquets és la comanda rpm que posseeix moltíssimes opcions. Internament rpm es basa en una base de dades amb informació sobre el instal · lat, les dependències existents, etc. Aquesta base de dades és actualitzada amb transparència pel rpm quan s'instal·la, s'actualitza o desinstal un paquet. També es pot consultar per conèixer informació diversa sobre el ja instal·lat en el sistema.

\begin{figure}
\centering
\includegraphics[width=11cm]{img/rpm.png}
\caption{La comanda rpm }
\end{figure}