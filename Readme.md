# Die eigene Nextcloud für zu Hause

# Einleitung

Wir werden einen **Nextcloud Server** auf einem **RaspberryPi** oder einem **Laptop**
einrichten. Das RaspberryPi ist ein Mikro-Computer wie man ihn ähnlich von der Leistung auch in einer TV-Box für digitales Fernsehen findet.  
Bei digitec gibt es das RaspberryPi 3+ Start Kit mit Adapter, Gehäuse und Memory Card.

Wenn du einen alten Laptop verwenden willst, installiere darauf **Linux Ubuntu 18.04 Desktop**
oder **Ubuntu 18.04 Server**. Wenn du das nicht selber tun kannst, kannst du den Laptop mitbringen.

Die erste Challenge: Einkauf tätigen oder alten Laptop vorbereiten (Neuinstallation des Betriebssystems Linux)

Für den Kurs müsst ihr ausserdem zu Hause bereits Vorbereitungen treffen, damit bei Start alle
die nötige Software installiert und die nötige Hardware dabei habt.

# Mitbringen

- RaspberryPi mit Raspian installiert oder Laptop mit einem Linux (Debian, Ubuntu, Mint, etc.), Strom Adapter und SD-Karte.
- eigener Laptop und Ladegerät, idealerweise hat der ein SD-Kartenlesegerät.
- RaspberryPi mit Daten-Festplatte oder zweiter Laptop mit einem Linux System.
- zusätzliche Backup-Festplatte oder USB-Stick zum Backupen strengstens empfohlen (min. 8 GB)

War seinen Router, dynDNS und Portforwarding sowie Aktivierung von ssh auf seinem Gerät im Griff hat, kann den Server auch gleich zu Hause vorinstallieren, um
danach nur noch die Installation per ssh zu machen.

## Anmerkung zur Hardware

Ich empfehle am ehesten, sich einen älteren Laptop oder auch PC Occasion zu kaufen.
Hier kann ich [Revamp IT](https://www.revamp-it.ch/index.php/en/) empfehlen, die dir ein gebrauchtes Gerät mit Linux zum guten Preis verkaufen. Sonst schaue bei [Ricardo](www.ricardo.ch) vorbei.

Ein komplettes RaspberryPi Set mit zusätzlicher Festplatte kommt fast  teurer als ein gebrauchter Laptop.
 
| RaspberryPi   | Laptop      | Desktop    |
| ------------- |-------------|------------|
| + sehr geringer Stromverbrauch (~2.5W)    | + geringer Stromverbrauch (~30W)  | - hoher Stromverbrauch
| + günstig (35 Fr. ohne Zubehör)    | - teurer (ab 100 bei Ricardo)   | - teurer (ab 100 bei Ricardo)
| + sehr klein und leise | + auch rel. klein und leise | - sperrig, evtl. laut...
| - max. 32 GB SD-Karte, zus. HD sehr empfohlen | + genügend Speicher onboard | + genügend Speicher onboard
| - geringere Zuverlässigkeit (z.B. Zeitraum 5 Jahre) | + grössere Zuverlässigkeit | + grössere Zuverlässigkeit
 Für einen wirklich produktiven Einsatz, wo die Cloud so richtig gefordert wird ist man auf die lange Sicht mit einem Laptop oder PC besser bedient. Auf www.ricardo.ch findet ihr geeignehnete, ältere Modelle, die sich sehr gut eignen.


Als Speicher für die Daten ist diese SD-Karte nicht geeignet. Es gibt grob 3 Speicher-Setups:
- externe Speichermedien wie eine **externe USB-Festplatte**.

- Sofern zu Hause ein sog. **Network Attached Storage (NAS)** vorhanden ist, kann dieser
als Hauptspeicher später verwendet werden.

- Es kann sogar ein Speicher von **Dropbox** oder **Google Drive** verwendet werden, und der 
Server legt die Daten dorthin verschlüsselt ab. Vorteil: Keine eigenen Backups nötig.

**Empfohlen:** eine zweite Festplatte oder USB-Stick für Backups. Lieber ein Laptop als ein RaspberryPi sofern vorhanden.

# Vorbereitung

Es mag sein, dass dir die Vorbereitung Mühe bereitet. Es bietet dir aber den Vorteil, offene Fragen am Workshop zu stellen. Ausserdem verhinderst du dadurch, dass du
an den Workshop kommst, die Cloud aber am Schluss doch nicht einsetzen kannst, da gewisse Schritte zu Hause gemacht werden müssen.

## 1. Kontrolle deines Routers zu Hause

Wenn du bei dir zu Hause eine Cloud einrichten willst, muss dein (WLAN)-Router gewisse Voraussetzungen erfüllen.

1. Er muss **dynamisches DNS** unterstützen. Denn deine IP-Addresse zu Hause wechselt alle Tage wieder. Die Nameszuordnung von z.B. 
**meinecloud.dyndns.org** mit deiner gerade aktuellen IP erfolgt durch einen solchen dynamischen DNS Dienst.

2. Er muss **Port-Forwarding** unterstützen (fast immer der Fall...). Wenn dann ein Webanfrage an deinen Server geschickt wird, gelangt er zu deinem Router. Für Webanfragen werden die Ports 80 (HTTP) und 443 (HTTPS) verwendet. Das Port-Forwarding ist die Einstellung, dass der Router alle Anfragen auf Port 80 und 443 auf die **lokale IP-Adresse deines Nextcloud-Servers** weiterleitet.

Nähere Infos, wie du dich beim Router einloggst, findest du unter `Doc/Login Router.md`.  

### DynDNS einstellen

Sobald du beim Router eingeloggt bist, suche in Einstellung nach **Dynamisches DNS** und schau, welche 
**DynDNS-Dienste** durch den Router unterstützt werden.

1. Wähle einen DynDNS-Dienstanbieter, z.B. https://www.noip.com/.
2. Erstelle einen Account.
3. Wähle die gewünschte Web-Adresse/URL für deine Cloud, z.B. **meinecloud.dyndns.org**.

Die URL benötigen wir später für die Cloud-Konfiguration. Sofern dies nicht geklappt hat, bitte vorher
bei mir melden. 

**Kontrolle nach ein paar Stunden**: Du solltest auf dem Terminal (Windows: `Ctrl+R` und dann cmd eingeben) deine Website "anpingen" können und daten zurück bekommen:

    $ ping ccczh.ch
    PING ccczh.ch (77.109.139.199) 56(84) bytes of data.
    64 bytes from www.ccczh.ch (77.109.139.199): icmp_seq=1 ttl=52 time=20.6 ms
    64 bytes from www.ccczh.ch (77.109.139.199): icmp_seq=2 ttl=52 time=19.9 ms
    64 bytes from www.ccczh.ch (77.109.139.199): icmp_seq=3 ttl=52 time=21.0 ms
    

Benutze `Ctrl + C` um das Ping zu beenden.

Wie in diesem Beispiel sieht man auch, welche IP-Addresse (77.109.139.199) sich hinter der Addresse verbirgt.




## Die Software

Ihr werden mit 2 Geräten arbeiten. Das eine ist euer Laptop. Dieser wird verwendet, um auf den späteren Server,
also das RaspberryPi zuzugreifen. Dieser Zugriff erfolgt über `ssh` (secure-shell). Einmal verbunden,
können wir dem Server über die Kommandozeile Befehle ausführen lassen, d.h. unsere Cloud installieren.

Auf deinem PC brauchts du nun einen **ssh-client**, der diese Verbindung aufbauen kann.

Windows: [Download Putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)  
Linux/Mac: ssh client ist bereits standardmässig dabei.

## URL für die Cloud definieren.

Um von überall auf der Welt auf die Cloud zu gelangen, stellen wir uns vor, unser Server ist ein Haus.
Dieses hat eine eindeutige Hausnummer, die sog. IP-Addresse z.b. 84.123.21.6.
Bei dir zu Hause wechselt die Hausnummer im Normalfall alle 24h, was man **dynamische IP** nennt. Professionelle Server
besitzen allerding statische IP's, die nicht wechseln.

Auch wenn die IP wechselt, müssen wir unserem Server eine URL geben wie z.B. **mycloud@mydomain.com**.
Wie können wir das erreichen?



Um unsere Cloud zu erreichen, müssen wir allerdings die 

## Dokumentation

Der Workshop ist in Sektionen aufgeteilt. Diese sind durchnummeriert. Zusätzlich gibts eine Ordner mit weiteren Themen,
die hilfreich sind, wenn ihr die Cloud einmal installiert habt. Auch Teil der Dokumentation sind verschiedene Scripte, 
die wir im Kurs benutzten. Diese enthalten ebenfalls hilfreiche Befehle

