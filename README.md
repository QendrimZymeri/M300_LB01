#  Modul 300 LB01

## Persönlicher Stand

Ich habe aus dem Betrieb schon einige Erfahrungen mit Virtualisierung gemacht.
Mit Vagrant habe ich bisher noch keine Erfahrungen gemacht.
Virtualisierung und die Automatisierung davon ist für mich aber ein sehr spannendes Thema und ich 
freue mich mehr darüber zu lernen und das in der Zukunft anzuwenden.

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


### SSH-Key hinzufügn auf SSH-Agent

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

### Reflexion

Im ganzen hat mir das Modul sehr Spass gemacht, auch wenn ich zu Beginn sehr viel Schwieriegkeiten hatte.
Dank diesem Modul, weiss ich jetzt wie man Vagrant-Files erstellt und sie anwendet. 
Das Vagrant hilft sehr und erleichtert die Aufgabe und spart sehr viel Zeit. Man kann in einem Vagrant-File mehrere Maschinen erstellen mit verschiedene Konfigurationen wie zB. Netzwerk usw. 
In der Zukunft werde ich sicherlich weiter mit Vagrant arbeiten und experimentieren. 
