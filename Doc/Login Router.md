## Login in den Router

Der Router ist das Gerät, das dir den Zugang zum Internet ermöglicht. Der Router bezieht vom
ISP (Internet Service Provider, z.B. Swisscom) automatisch eine IP, soz. die Hausnummer.
Wenn sich zu Hause deine verschiedenen Geräte mit dem Router verbinden, **vergibt der Router jedem Gerät eine IP im lokalen Netzwerk**, 
welches **LAN (Local Area Network)** gennant wird.
Der Router selber hat die Addresse `192.168.0.1` oder `192.168.1.1`, die restlichen Geräte eine Addresse `192.168.0.x` oder `192.168.1.x`,
wobei x zwischen 0 bis 255 liegen kann.

Sobald du mit deinem Router über WLAN oder Kabel verbunden bist, kannst du dich über die seine **lokale IP** mit ihm verbinden.
Gehe in deinen Inter-Browser und gib die Addresse `192.168.0.1` oder `192.168.1.1` ein.

Ansonsten hilft dir auf Windows folgendes, um die IP herauszufinden:

Drücke `Ctrl+R` und gib cmd ein, um eine Kommandozeile zu starten. Tippe `ipconfig /all`.

und suche den Netzwerk-Adapter, mit dem du verbunden bist. Die gesuchte IP ist der standardGateway.
Auf Linux findest das lokale Netz mit `ifconfig`.  

Oft ist der Benutzername `admin`, das Passwort für das Login kann

- auf deinem Router aufgeklebt sein (z.B. wenn identisch mit dem Standard-WLAN-Password)
- ein Standard-Passwort sein (`admin` oder `1234`), falls, unbedingt gleich anpassen und ein sicheres verwenden.