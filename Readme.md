# Die eigene Nextcloud für zu Hause

# Einleitung

Wir werden einen **Nextcloud Server** auf einem **RaspberryPi** oder einem **Laptop**
einrichten. Das RaspberryPi ist ein Mikro-Computer sowie etwa TV-Box für digitales Fernsehen.

Für diejenigen, die noch nie Befehle in eine Kommando-Zeile eingegeben haben, wird vieles neu sein.
Mithilfe der Dokumentation kann aber jederzeit nachvollzogen werden, was die einzelnen Schritte sind.

Für den Kurs müsst ihr ausserdem zu Hause bereits Vorbereitungen treffen, damit bei Start alle
die nötige Software installiert und die nötige Hardware dabei habt.


# Vorbereitung

## Die Hardware

Ich empfehle ein RaspberryPi Starter Kit für ca. 70 Franken, da 

1. es sehr wenig Strom verbraucht,
2. für ein voll funktionsfähiger Computer sehr günstig ist,
3. das Betriebsystem liegt auf einer Micro-SD-Speicherkarte und kann einfach
ausgetauscht werden. Das RaspberryPi kann auch für andere Dinge verwendet werden.
4. Das offizielle Operating System für RaspberryPi ist **Raspian** und ist im Startkit dabei.

Als Speicher für die Daten ist diese SD-Karte nicht geeignet. Es gibt grob 3 Speicher-Setups:
- externe Speichermedien wie eine **externe USB-Festplatte** oder **mehrere USB Sticks**.

- Sofern zu Hause ein sog. **Network Attached Storage (NAS)** vorhanden ist, kann dieser
als Hauptspeicher später verwendet werden.

- Es kann sogar ein Speicher von **Dropbox** oder **Google Drive** verwendet werden, und der 
Server legt die Daten dorthin verschlüsselt ab. Vorteil: Keine eigenen Backups nötig.

**Empfohlen:** eine zweite Festplatte oder USB-Stick für Backups.

## Die Software

Ihr werden mit 2 Geräten arbeiten. Das eine ist euer Laptop. Dieser wird verwendet, um auf den späteren Server,
also das RaspberryPi zuzugreifen. Dieser Zugriff erfolgt über `ssh` oder secure-shell. Einmal verbunden,
können wir dem Server über die Kommandozeile Befehle ausführen lassen, d.h. unsere Cloud installieren.

Auf deinem PC brauchts du nun einen **ssh-client**, der diese Verbindung aufbauen kann.

Windows: [Download Putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)  
Linux/Mac: ssh client ist bereits standardmässig dabei.


# Mitbringen


- eigener Laptop und Ladegerät
- RaspberryPi mit Daten-Festplatte oder zweiter Laptop mit einem Linux System.
- zusätzliche Backup-Festplatte

## Dokumentation

Der Workshop ist in Sektionen aufgeteilt. Diese sind durchnummeriert. Zusätzlich gibts eine Ordner mit weiteren Themen,
die hilfreich sind, wenn ihr die Cloud einmal installiert habt. Auch Teil der Dokumentation sind verschiedene Scripte, 
die wir im Kurs benutzten. Diese enthalten ebenfalls hilfreiche Befehle

