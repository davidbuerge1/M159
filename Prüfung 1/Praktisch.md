# AD Grundlagen
## Die Lernenden installieren einen AD Server gemäss Anleitung.

### VM starten und initiale Konfiguration

1. **VM starten**: Play virtual machine von `C:\VMs\WS4V...`
2. **Anmelden**:
   - Melden Sie sich als lokaler Administrator mit dem Passwort `Riethuesli>12345` an.
   - Falls nötig, ändern Sie das Passwort auf `C0mplex` (das 2. Zeichen ist hier eine Null). Merken Sie sich Ihr Passwort genau.
3. **Kontrolle des Tastatur-Layouts**:
   - Öffnen Sie **Windows PowerShell (PS)**.
   - Falls anstelle des Buchstabens `+` mit `<SHIFT><1>` etwas anderes erscheint, passen Sie das Tastatur-Layout wie folgt an:
     1. Start | **Control Panel** | Kategorie: auf **Small icons** setzen | **Language**
     2. Unter **Change your language preferences** wählen Sie **Add a language** | **Deutsch (Schweiz)** und klicken Sie auf **Add**.
     3. Die Zeile **Deutsch (Schweiz)** selektieren und mit **Move up** nach oben verschieben.
     4. **Change date, time, or number formats** | Registerkarte **Location**: Wählen Sie **Switzerland** und bestätigen Sie mit **OK**.
     5. Überprüfen Sie unter **Settings** (am rechten Rand), ob das ENGLISH-Tastatur-Layout immer noch geladen ist. Falls ja, starten Sie die VM neu.
     6. In der Statusleiste am unteren Fensterrand sollte nun **DEU** als Tastatur-Layout angezeigt werden.
4. **Server Manager öffnen**:
   - Öffnen Sie die zentrale Verwaltungskonsole **Server Manager** und wählen Sie im linken Fenster **Local Server**.
   - Unter **PROPERTIES** erscheint **Ethernet**. Klicken Sie auf den Link **IPv4 address assigned by DHCP…** und dann auf **Network Connections**.
   - Doppelklicken Sie auf die **1 Ethernet0-Karte** und gehen Sie zu **Properties**:
     - Deaktivieren Sie **Internet Protocol Version 6 (TCP/IP)**.
     - Wählen Sie **Internet Protocol Version 4 (TCP/IP)** | **Properties** und setzen Sie folgende Werte:
       - IP-Adresse: `10.x.230.10 / 255.255.255.0` (x ist Ihre spezifische Zahl)
       - Gateway: `10.x.230.1` (Dieser Eintrag spielt vorerst keine Rolle.)
       - DNS-Server: `10.x.230.10` (Der eigene Server wird DNS-Server; DC ist auch DNS-Server.)
5. **Firewall abschalten**:
   - Im **Server Manager** klicken Sie auf den Link bei **Turn Windows Firewall on or off** und schalten die Firewall für das private und das öffentliche Netzwerk ab.
6. **Computernamen ändern**:
   - Im **Server Manager** ändern Sie den Computernamen auf **ADSERVER** (zweimal ändern). Die **Workgroup** bleibt unverändert.
7. **VM neu starten**.

### AD-Rolle installieren

1. **AD-Rolle hinzufügen**:
   - Öffnen Sie **Server Manager** und gehen Sie zu **Local Server**.
   - Wählen Sie **Manage | Add Roles and Features** | **Next**.
   - Wählen Sie **Role-based or feature-based installation** und **Select a server from the server pool**.
   - Wählen Sie unseren Server aus und setzen Sie die Checkbox für **Active Directory Domain Services**.
   - Klicken Sie auf **Add Features** und dann auf **Next**.
   - Überprüfen Sie die Features und klicken Sie auf **Next** und **Install**.
   - Falls gewünscht, wählen Sie die Option **Restart the destination server automatically if required**.
   - Klicken Sie auf **Install**. 
   - Vor dem Abschluss der Installation können Sie mit **Export Configuration Settings** die Einstellungsdaten als **DeploymentConfigTemplate.xml** speichern. Schließen Sie das Fenster mit **Close**.

### Server zu DC heraufstufen

1. **Heraufstufen zum Domain Controller**:
   - Warten Sie, bis im **Server Manager** ein Rufezeichen erscheint.
   - Klicken Sie auf das Rufezeichen und dann auf **Promote this server to a domain controller**.
   - Unter **Deployment Configuration** wählen Sie **Add a new forest** und geben Sie den **Root domain name** `y.demo` als FQDN ein.
     - Hinweis: Top-Level-Domains, die im Internet nicht vorkommen, werden verwendet, um Verwechslungen zu vermeiden.
   - Belassen Sie **Forest und Domain functional level** auf **Windows Server 2019**.
   - Geben Sie das Wiederherstellungspasswort ein, z.B. `Riethuesli>12345`. Dieses Passwort wird nur benötigt, wenn das AD von einem Backup wiederhergestellt werden muss.
   - Bestätigen Sie, dass die Parent Zone **verein** nicht gefunden wurde. Dies ist beabsichtigt.
   - Belassen Sie **NetBIOS** auf dem Standardwert und klicken Sie auf **Next**.
   - Unter **Paths** können Sie die Verzeichnisse für AD DS-Datenbank, Protokolldateien und SYSVOL anpassen oder auf den Standardwert belassen:
     - Database folder und Log files folder: `C:\Windows\NTDS`
     - SYSVOL folder: `C:\Windows\SYSVOL`
   - Klicken Sie auf **View script**, um die Konfigurationsdaten in eine Datei zu speichern. Notepad öffnet sich. Speichern Sie die Datei ohne Passwörter.
   - Überprüfen Sie die **Check-Resultate** und klicken Sie auf **Install**.
   - Warten Sie, bis die Installation abgeschlossen ist und starten Sie den Server neu.
   - Melden Sie sich als Domänenadministrator an und ändern Sie ggf. das Passwort.


## Sie konfigurieren den AD-Schema-Editor als MMC-Snap-In und finden Eigenschaften von Klassen sowie Attributen im Tool.  
1. Ausführen in Konsole ```regsvr32 schmmgmt.dll ```
2. öffnen in MMC [![Mein Bild](https://example.com/mein-bild.png)](https://github.com/benutzername/repository)

## Sie legen einen Computer, Benutzer, etc. im Attribut-Editor an und überprüfen diese. 
1. öffnen in MMC [![Mein Bild](https://example.com/mein-bild.png)](https://github.com/benutzername/repository)
2. öffnen in MMC [![Mein Bild](https://example.com/mein-bild.png)](https://github.com/benutzername/repository)
3. öffnen in MMC [![Mein Bild](https://example.com/mein-bild.png)](https://github.com/benutzername/repository)


## Sie verstehen die Wechselwirkung zwischen Schema- und Attribut-Editor.
1. Schema definiert die Rahmenbedinnungen 
2. Einschränkung durch schema BSP. EInschränkung für attribute -> nur Ganzzahlen
3. Wird etwas am Schema geändert, so passt sich der Attribut editor an. 

# Entwurf AD

## Die Lernenden planen ein einfaches Directory Service Konzept, d.h. sie kennen die Best-Practise Methoden und Merkregeln für die logische und physische Sicht. Sie lösen Fallbeispiele und berechnen die Mindestanzahl von DC’s und definieren Domänenbezeichnungen.

