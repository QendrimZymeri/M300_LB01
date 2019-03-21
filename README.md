#  Modul 300 LB01

## Persönlicher Stand

Ich habe aus dem Betrieb schon einige Erfahrungen mit Virtualisierung gemacht.
Mit Vagrant habe ich bisher noch keine Erfahrungen gemacht.
Virtualisierung und die Automatisierung davon ist für mich aber ein sehr spannendes Thema und ich 
freue mich mehr darüber zu lernen und das in der Zukunft anzuwenden.

Github hatte ich noch nie zuvor benutzt.Ehrlich gesagt habe ich nicht gewusst was das ist.
### Einrichten

## Git bash

1. Git bash herunterladen 
2. Git bash installieren

Anschliessend wird noch das Repository auf den lokalen Computer kopiert.
```
$ git clone https://github.com/mc-b/M300      #Repository klonen
 ```
  
## GitHub Account

1. GitHub Account erstellen
2. Mit Git bash SSH Key erstellen
3. SSH Key dem Agent hinzufügen
4. SSH Key dem GitHub Konto hinzufügen

## Virtualbox

1. Virtualbox herunterladen
2. Virtualbox installieren

## Visual Studio Code

1. Visual Studio Code herunterladen
2. Visual Studio Code installieren
3. Extensions installieren
4. Einstellungen anpassen

## Vagrant

1. Vagrant herunterladen
2. Vagrant installieren
3. Vagrant VM erstellen

Eine VM kann mit Vagrant wie folgt erstellt werden:
    
    $ mkdir vagrantvm                                                                       #Ordner für die VM erstellen
    $ cd vagrantvm                                                                          #In verzeichniss wechseln
    $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Repository in den Ordner kopiert
    $ vagrant init ubuntu/xenial64                                                          #Vagrantfile erstellen
    $ vagrant up --provider virtualbox                                                      #Virtuelle Maschine erstellen & starten
    
Danach ist die VM in Virtualbox ersichtlich und kann benützt werdenVa

# Vagrant Befehle

Hier sind die wichtigsten Vagrant Befehle aufgelistet:

| Befehl           |Beschreibung                                                                             |
| -----------------|:---------------------------------------------------------------------------------------:|
| Vagrant init     |Initialisiert die Vagrant Umgebung im aktuellen Verzeichnis und erstellt ein Vagrantfile |
| Vagrant up       |Erzeugt und Konfiguriert eine Virtuelle Maschine basierend auf dem Vagrantfile           |
| Vagrant ssh      |Verbindung zur VM per SSH wird hergestellt                                               | 
| Vagrant status   |Zeigt den aktuellen Status der VM an                                                     | 
| Vagrant port     |Zeigt die Weitergeleiteten Ports der VM an                                               | 
| Vagrant halt     |VM wird gestoppt                                                                         | 
| Vagrant destroy  |VM wird gestoppt und gelöscht                                                            | 

## Webserver

Der Webserver kann anschliessend auf der VM installiert werden. Dazu wird folgender Befehl verwendet.
```
   $ sudo apt-get install apache2
```
Da wir dies aber automatisieren wollen, können wir den schnelleren, einfacheren Weg über Vagrant benützen.
```
   $  cd m300/vagrant/web
   
   $  vagrant up
   ``` 
Anschliessend ist der Webserver installiert und kann auf der VM im Webbrowser unter http://127.0.0.1 erreicht werden.



## Firewall und Reverse Proxy

   Für die Firewall wird ufw verwendet, diese kann ganz eifach per Command Line installiert werden.
   
    $ sudo apt-get install ufw
    
 ## SSH-Key
 
 Man benötigt den SSH-Key, damit man eine sichere Verbindung zum Repository macht. 
 
 #### Wie erstellt man diesen Key?
 
1. Git Bash öffnen

2. Den Befehl eingeben und die gewünschte E-Mail Adresse einfügen 
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

3. Diese Befehl erstelt einen neuen SSH-Key
```> 
Generating public/private rsa key pair.
```


4. Dannach fragt das System, wo man das File Sichern möchte
```> 
Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
```

5. Zum Schluss wird das System noch fragen, ob man das File mit einem Password schützt
```sh  Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

So Sieht der Key aus:

```sh

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDJkTb63o9dO/BeQGwcSYDqa1/gkqOOWI2ud97SSxYrXrpd0TX1zPpmOZ0Kf+
/1MdmDYpLOPYX6F1gMcTLPoFcES2h8n7UZT4ioVsVkKq4ad7/KYmChgkiEoVzRhnLmNpQEbF1mk/+zKZWwAYq4b/XN/zd83HDOWX4mtrn
/8OJiup+jFSFcyVG5GNZQUmPsxeOuYNE+qrMdn07PevoxI5bjlI/+Gr/IFc4bkN3QQ2AedaNZ+MyJ7Cr1ttZKyoIWNpiTvsjbWSLzMSSchl+iThO6/rQQdHrZaXuB7ApV3CdQq
/htYMvwSW9khSWHTABEAG1UKqYDfGXtyII6se7SE1B7pYeieDhsY4hbqTpcetc4PqTGRI5Vc9A5NyyXjnRDuBaIFJ28c9Thg1zm7aCPRkwtF0x0D34uF6yVGtbFlpqhreQ+b2ml
/eBccJOaABgwD7niG5TYig59uFKqtXlgXnbnQmM2FTQqdKHD6TppdZhiB/crQPxZpGOqOq6N4ch7R0k95LFgzlgaXzkvbsR7dRtu4+d7gnfD/cksjG
/zZaZJcxzbZQKWJoxWASOfa30SDxeksCX+OZMA4a40STmOmNtfQjP9aCZJkUQ9dYODoYKhT1WpfiXhh4hY0E4oGYgX4EOAk2hMF6FEN6Pow== 
/sx0tMLgUy82wJ3IKF2t00llzJG2Lqendrim.zymeri@hotmail.com

```


### SSH-Key hinzufügen auf SSH-Agent

1. Sicherstellt, dass der SSH-Agent läuft
2. Diesen Befehl ausführen:
```
# start the ssh-agent in the background
$ eval $(ssh-agent -s)
> Agent pid 59566
```
3. Den SSH-Key am SSH-Agent hinzufügen
```
$ ssh-add ~/.ssh/id_rsa
```

### Vagrant-Übung

Zuerst habe ich eine Multi VM Umgebung aufgebaut. Das Vagrant-File konnten wir vom Repository von Herrn Kählin downloaden.

```
+---------------------------------------------------------------+
! Notebook - Schulnetz 10.x.x.x und Privates Netz 192.168.55.1  !                 
! Port: 8080 (192.158.55.101:80)                                !	
!                                                               !	
!    +--------------------+          +---------------------+    !
!    ! Web Server         !          ! Datenbank Server    !    !       
!    ! Host: web01        !          ! Host: db01          !    !
!    ! IP: 192.168.55.101 ! <------> ! IP: 192.168.55.100  !    !
!    ! Port: 80           !          ! Port 3306           !    !
!    ! Nat: 8080          !          ! Nat: -              !    !
!    +--------------------+          +---------------------+    !
!                                                               !	
+---------------------------------------------------------------+
```

1. Web Server mit Apache und MySQL UserInterface Adminer
2. Datenbank Server mit MySQL
3. Die Verbindung Web - Datenbank erfolgt mittels Internen Netzwerk Adapter.
4. Von Aussen ist nur der HTTP Port auf dem Web Server Erreichbar.

Um in die VM zu wechseln ist zusätzlich der in Vagrantfile definierte Name einzugeben.
```
vagrant ssh database
```
```
vagrant ssh web
```

### Eigenes Vagrant

```
+---------------------------------------------------------------+
! Notebook - Schulnetz 10.x.x.x und Privates Netz 192.168.6.1   !                 
! Port: 8080 (192.158.6.101:80)                                 !	
!                                                               !	
!    +--------------------+          +---------------------+    !
!    ! Appache Server     !          ! DHCP Server         !    !       
!    ! Host: appache      !          ! Host: db01          !    !
!    ! IP: 192.168.6.7    ! <------> ! IP: 192.168.6.5     !    !
!    ! Port: 80           !          !                     !    !
!    ! Nat: 8080          !          !                     !    !
!    +--------------------+          +---------------------+    !
!                                                               !
!                                                               !
!                                                               !
!                  +---------------------+                      !
!                  ! FTP Server          !                      !
!                  ! Host: ftp           !                      !
!                  ! IP: 192.168.6.6     !                      !
!                  ! Port 3306           !                      !
!                  ! Nat: -              !                      !
!                  +---------------------+                      !                                                           
!                                                               !
!	                                                              !
+---------------------------------------------------------------+
```




DHCP-Server
-------------
Die DHCP VM hat folgende Spezifikationen (Die Änderungen kann man im Vagrant-File vornehmen):
* IP: 192.168.6.5
* Hostname: dhcp
* RAM: 1024 MB
* VM Box: Ubuntu

```
config.vm.define "dhcp" do |dhcp|
  dhcp.vm.box = "ubuntu/xenial64"
  dhcp.vm.hostname = "dhcp"
  dhcp.vm.network "private_network", ip:"192.168.6.5" 
	dhcp.vm.provider "virtualbox" do |vb|
	  vb.memory = "1024"  
end  
```
Der erstes Schritt ist die Paketverzeichnis aktualisiert wird. 

```
sudo apt-get update
```
Im nächsten Schritt wird eine Gruppe mit inklusvie Benutzer mit Passwort erstellt. Es sieht so aus: 
```
#Gruppe Myadmin erstellen
sudo groupadd myadmin
#User erstellen
sudo useradd admin -g myadmin -m -s /bin/bash
sudo useradd test -g myadmin -m -s /bin/bash
#Password festlegen
sudo chpasswd <<<admin:admin
sudo chpasswd <<<test:test
```
Bei nächsten Schritt wird der DHCP Server installiert. Das Paket lautet: ISC-DHCP-SERVER.
```
sudo apt-get -y install isc-dhcp-server
```
Nach der Installation von DHCp-Server muss man die Konfiguration anpassen. Das Konfigurationfile vom DHCP Server befindet sich im Pfad /etc/dhcp/dhcpd.conf. Bei dem Konfigurationfile wird folgendes geändert:
* Domainname
* DNS
* DHCP Scope

Der Domainname lautet Standardmässig example.org und will neu labor.local umändern. 
```
#Domainanme konfigurieren
sudo sed -i 's/example.org/labor.local/g' /etc/dhcp/dhcpd.conf
```
Der DNS wird nun auf 8.8.8.8 (Google DNS) konfiguriert.
```
#DNS konfigurieren
sudo sed -i 's/ns2.labor.local/8.8.8.8/g' /etc/dhcp/dhcpd.conf
```
Im Bereich beim Scope hat folgende Parameter:
* Subnet --> 192.168.6.0/24
* Range --> 192.168.6.100 - 130
* Gateway --> 192.168.6.1
```
#DHCP Autorisierung aktiviert
sudo sed -i 's/#authoritative/authoritative/g' /etc/dhcp/dhcpd.conf
#DHCP Subnetz & Maske konfigurieren
sudo sed -i '$asubnet 192.168.6.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf
#DHCP Range konfigurieren
sudo sed -i '$arange 192.168.6.100 192.168.6.130;' /etc/dhcp/dhcpd.conf
#DHCP Gateway konfigurieren
sudo sed -i '$aoption routers 192.168.6.1;' /etc/dhcp/dhcpd.conf
sudo sed -i '$a}' /etc/dhcp/dhcpd.conf
```
Nach der Änderung des Konfigurationsfile wird der DHCP Service neu gestartet.
```
#DHCP Server neustarten
sudo service isc-dhcp-server restart
```
Die Tastaturlayout muss man noch auf Deutsch Schweiz anpassen.
```
#Tastaturlayout anpassen
sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
```
Am Ende wird noch eine lokale Firewall installiert und anschliessend auch konfiguriert. Dabei öffnen man den Port 22 um via SSH darauf zuzugreifen. INFO-INPUT SSH Port 22 | TELNET Port 23
```
#Local Firewall installieren
sudo apt-get -y install ufw gufw 
sudo ufw allow from 10.0.2.2 to any port 22
sudo ufw --force enable    
```
Nun ist die DHCP-Part abgeschlossen. Man kann jetzt Clients VM erstellen und mit dem DHCP-Server innerhalb IP-Range IP-Adresse bekommen.

FTP-Server
----------
Die FTP VM hat folgende Spezifikationen (Die Änderungen kann man im Vagrant-File vornehmen):
* IP: 192.168.6.6
* Hostname: ftp
* RAM: 1024 MB
* VM Box: Ubuntu

```
config.vm.define "ftp" do |ftp|
  ftp.vm.box = "ubuntu/xenial64"
  ftp.vm.hostname = "ftp"
  ftp.vm.network "private_network", ip: "192.168.6.6"
  ftp.vm.network "forwarded_port", guest:3306, host:3306, auto_correct: true
  ftp.vm.provider "virtualbox" do |vb|
	 vb.memory = "1024"  
end
```
Der erstes Schritt ist erneut die Paketverzeichnis zu akualisieren. 

```
sudo apt-get update
```
Bei nächsten Schritt wird der FTP Server installiert. Das Paket lautet: pure-ftpd
```
#FTP Server installieren
sudo apt-get -y install pure-ftpd-common pure-ftpd
```
Nach der Installation kann ich die FTP-Server konfigurieren. Bei meinem Fall sieht es so aus: 
```
sudo groupadd ftpgroup
sudo useradd -g ftpgroup -d /dev/null -s /etc ftpuser
sudo pure-pw useradd qendrim -u ftpuser -g ftpgroup -d /home/pubftp/qendrim -N 10
```
Nach der Änderung wird der FTP Service neu gestartet.
```
#FTP Server neustarten
sudo service pure-ftpd-common pure-ftpd restart
#sudo /home/pubftp/qendrim restart
```
Die Tastaturlayout muss man noch auf Deutsch Schweiz anpassen.
```
#Tastaturlayout anpassen
sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
```
Am Ende wird noch eine lokale Firewall installiert und anschliessend auch konfiguriert. Dabei öffnen man den Port 22 um via SSH darauf zuzugreifen. INFO-INPUT SSH Port 22 | TELNET Port 23
```
#Local Firewall installieren
sudo apt-get -y install ufw gufw 
sudo ufw allow from 10.0.2.2 to any port 22
sudo ufw --force enable    
```
Nun ist die FTP-Part abgeschlossen.

Apache-Server
----------
Die Apache VM hat folgende Spezifikationen (Die Änderungen kann man im Vagrant-File vornehmen):
* IP: 192.168.6.7
* Hostname: apache
* RAM: 1024 MB
* VM Box: Ubuntu

```
config.vm.define "apache" do |apache|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "apache"
  config.vm.network "private_network",ip:"192.168.6.7",netmask:"255.255.255.0",default_gateway:"192.168.6.1"
  config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
  config.vm.synced_folder ".", "/var/www/html"
  config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
end
```
Der erstes Schritt ist ebenfalls erneut die Paketverzeichnis zu aktualisieren. 

```
sudo apt-get update
```
Im nächsten Schritt wird eine Gruppe mit inklusvie Benutzer mit Passwort erstellt. Es sieht so aus: 
```
#Gruppe Myadmin erstellen
sudo groupadd myadmin
#User erstellen
sudo useradd admin -g myadmin -m -s /bin/bash
sudo useradd test -g myadmin -m -s /bin/bash
#Password festlegen
sudo chpasswd <<<admin:admin
sudo chpasswd <<<test:test
```
Bei nächsten Schritt wird der Apache Server installiert und die Service wird neugestartet. Das Paket lautet: apche2
```
#Installation Apache2
sudo apt-get -y install apache2
#Apache2 Service neustarten
sudo service apache2 restart
```
Die Tastaturlayout muss man noch auf Deutsch Schweiz anpassen.
```
#Tastaturlayout anpassen
sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
```
Am Ende wird noch eine lokale Firewall installiert und anschliessend auch konfiguriert. Dabei öffnen man den Port 22 um via SSH darauf zuzugreifen. INFO-INPUT SSH Port 22 | TELNET Port 23
```
#Local Firewall installieren
sudo apt-get -y install ufw gufw 
sudo ufw allow from 10.0.2.2 to any port 22
sudo ufw --force enable    
```
Nun ist auch die Apache-Part abgeschlossen.

##### Sicherheit
```
Datenbank Server bzw. MySQL ist mit Password geschützt.
Der Web Server ist offen und mittels ungeschütztem HTTP Protokoll erreichbar.
```

### K1
1. VirtualBox
2. Vagrant
3. Visualstudio-Code
4. Git-Client
  Der Git-Client wird verwendet. Ich habe mein Repository damit verknüpft und sobald ich lokal auf dem Pc (Ausgewählten Order) etwas     
  ändere, wird’s automatisch in meinem Repository synchronisiert.
5.	SSH-Key für Client erstellt



### K2
1. GitHub oder Gitlab-Account ist erstellt
https://github.com/QendrimZymeri/M300_LB01
2. Git-Client wurde verwendet
3. Dokumentation ist als Mark Down vorhanden
Ich habe mich entschieden die Doku in Word zu machen und diese Word-Datei später im Repository hochzuladen. Es fiel mir am Beginn etwas schwierig mit dem Mark Down zu arbeiten, da es speziell formatiert worden ist. 
4. Mark down-Editor ausgewählt und eingerichtet8
5. Mark down ist strukturiert

6. Persönlicher Wissenstand im Bezug auf die wichtigsten Themen sind dokumentiert (Linux, Virtualisierung, Vagrant, Versionsverwaltung / Git, Mark Down, Systemsicherheit)
Im Betrieb arbeite ich täglich mit Virtuellen Server (ESXI Umgebung). Da mir Vagrant sehr fremd war, fragte ich in der Firma nach, ob sich jemand mit Vagrant auskennt. Leider kannte sich niemand im Team mit Vagrant aus. Dank den ersten Input von Herr Kählin über Vagrant, konnte ich meinen Teamkollegen erzählen was Vagrant ist und was es so macht. Sie fanden das sehr spannend. 


7. Wichtige Lernschritte sind dokumentiert





### K3
1. Bestehende vm aus Vagrant-Cloud einrichten
Am 2. Tag mussten wir einen Vorgegebenen Vagrant-File von der Lehrperson Downloaden und das Vagrant-File ausführen. Zu Beginn war das ein bisschen kompliziert, da der Pfad stimmen musste usw. Jedoch heute fälölt mir das sehr leicht.
2. Kennt die Vagrant-Befehle
3. Eingerichtete Umgebung ist dokumentiert (Umgebungs-Variablen, Netzwerkplan gezeichnet, Sicherheitsaspekte)
4. Funktionsweise getestet inkl. Dokumentation der Testfälle
5. andere, vorgefertigte vm auf eigenem Notebook aufgesetzt
6. Projekt mit Git und Mark Down dokumentiert


### K4
1. Firewall eingerichtet inkl. Rules
2. Reverse-Proxy eingerichtet
3. Benutzer- und Rechtevergabe ist eingerichtet
4. Zugang mit SSH-Tunnel abgesichert
5. Sicherheitsmassnahmen sind dokumentiert
6. Projekt mit Git und Mark Down dokumentiert

### K5

Allgemein

1. Kreativität
2. Komplexität
3. Umfang

Umsetzung eigener Ideen
1. Cloud-Integration (Einsatz einer IaaS-Umgebung)
2. Authentifizierung und Autorisierung via LDAP
3. Übungsdokumentation als Vorlage für Modul-Unterlagen erstellt 

Persönliche Lernentwicklung
1. Vergleich Vorwissen - Wissenszuwachs
2. Reflexion

### Wissenszuwachs
Ich kann jetzt ein eigenes Vagrant-File erstellen und zum laufen bringen, was ich zu Beginn nicht konnte. Was ich auch noch dazu gelernt habe ist das mit dem Git-Hub. Ich finde es ist ein gutes "Tool" um Dokumentationen dort zu ablegen. 


### Reflexion

Im ganzen hat mir das Modul sehr Spass gemacht, auch wenn ich zu Beginn sehr viel Schwieriegkeiten hatte.
Dank diesem Modul, weiss ich jetzt wie man Vagrant-Files erstellt und sie anwendet. 
Das Vagrant hilft sehr und erleichtert die Aufgabe und spart sehr viel Zeit. Man kann in einem Vagrant-File mehrere Maschinen erstellen mit verschiedene Konfigurationen wie zB. Netzwerk usw. 
In der Zukunft werde ich sicherlich weiter mit Vagrant arbeiten und experimentieren. 
