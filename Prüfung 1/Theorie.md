# Lernziele Prüfung I: M159 Directory Services

## Lernziele: Schriftlicher Teil

### 1. Was ist ein Verzeichnisdienst?
Die Lernenden erklären die Funktionsweise und den Einsatz eines Directory Services.

#### Funktionsweise eines Directory Services:
1. **Zentrale Datenbank**: Der Directory Service verwendet eine zentrale Datenbank, in der Informationen wie Benutzerkonten, Gruppen, Computer, Drucker und andere Ressourcen gespeichert werden. Diese Datenbank ist in einer hierarchischen Struktur organisiert, ähnlich wie ein Dateisystem.
2. **Authentifizierung**: Der Directory Service überprüft die Identität von Benutzern, die auf Netzwerkressourcen zugreifen möchten. Dies erfolgt in der Regel durch die Eingabe eines Benutzernamens und eines Passworts.
3. **Autorisierung**: Nach der Authentifizierung bestimmt der Directory Service, auf welche Ressourcen der Benutzer zugreifen darf. Dies wird durch Richtlinien oder Zugriffssteuerungslisten (ACLs) geregelt.
4. **Verzeichnisprotokolle**: Directory Services verwenden oft Protokolle wie LDAP (Lightweight Directory Access Protocol), um auf die Verzeichnisinformationen zuzugreifen und diese zu verwalten.

#### Einsatz eines Directory Services:
- **Benutzerverwaltung**: Ein Directory Service ermöglicht die zentrale Verwaltung von Benutzern und deren Zugriffsrechten auf Netzwerkressourcen. Dies ist besonders in großen Organisationen nützlich.
- **Netzwerksicherheit**: Authentifizierungs- und Autorisierungsfunktionen verbessern die Netzwerksicherheit.
- **Skalierbarkeit**: Directory Services sind in der Lage, große Netzwerke mit vielen Benutzern und Ressourcen effizient zu verwalten.
- **Beispiele für Directory Services**: Microsoft Active Directory (AD), OpenLDAP, Novell eDirectory.

### 2. Skalierbarkeit, Erweiterbarkeit, Sicherheit, Verfügbarkeit und Performance eines Directory Services
- **Skalierbarkeit**: Verzeichnisse sollten große Datenmengen aufnehmen können.
- **Erweiterbarkeit**: Zusätzliche Objekttypen und Inhaltsstrukturen können eingefügt werden.
- **Sicherheit**: Der Zugriff auf die Informationen muss für autorisierte Personen gewährleistet sein.
- **Verfügbarkeit**: Benutzer müssen ständig auf aktuelle Daten zugreifen können.
- **Performance**: Der Zugriff auf Daten sollte schnell und zuverlässig erfolgen.

### 3. Standards: X.500, DNS und LDAP im MS Active Directory
- **X.500**: Dezentraler Aufbau, einheitlicher Namenskontext, Datenstruktur ist erweiterbar.
- **DNS**: Das AD baut auf dem DNS auf. Der FQDN lautet z.B.: `gbs.nesa-sg.ch`.
- **LDAP**: Industriestandard von IETF, Zugriff von Fremdsystemen auf AD, Speicherung in einer hierarchischen Struktur.

### 4. X.500 Standard
Die Lernenden verstehen die Namensbildung (DN, RDN), den Schemaaufbau mit Objektklassen und die Eigenschaften der Attribute.

#### Namensbildung
- **Distinguished Name (DN)**: Der eindeutige Name eines Objekts, zusammengesetzt aus verschiedenen Ebenen.
- **Relative Distinguished Name (RDN)**: Name in einer Ebene, z.B. `CN=Max Mustermann, OU=IT-Abteilung, O=Beispiel GmbH, L=Berlin, C=DE`.

#### Klassen und Attribute
- **Attribute** definieren die Eigenschaften von Feldern der Klassen, z.B. Byte, numerisch, Unicode-Zeichenfolge.
- **Klassen** definieren Eigenschaften von Objekten, z.B. Computer, Benutzer, Standort.

#### OID (Object Identifier)
Ein eindeutiger hierarchisch strukturierter Bezeichner, verwendet in LDAP, SNMP und X.509-Zertifikaten.

#### Replikationsmodelle
- **Single-Master-Replikation (X.500)**: Ein Primary und mehrere Secondary, Änderungen nur im Primary.
- **Multi-Master-Replikation (AD)**: Mehrere Master verwalten das Original, Konflikte müssen geregelt werden.

### 5. Domain Name System (DNS)
Die Lernenden kennen den hierarchischen Aufbau und die Eigenschaften des DNS:
- **Eigenschaften**: Basierend auf TCP/IP-Protokoll. Die Domäne `nesa-sg.ch` kann Subdomänen wie `gbs` enthalten. Der FQDN lautet: `gbs.nesa-sg.ch`.

#### Zonentypen im DNS
1. **Primäre Zone**: Enthält das Original der Zonendaten.
2. **Sekundäre Zone**: Enthält eine Kopie der Zonendaten und fragt periodisch beim Primary nach Updates.

### 6. Domäne und Standort
#### Domänenmodell
- **Sicherheitsgrenzen**: Domänengrenzen sind Sicherheitsgrenzen, der Admin der übergeordneten Domäne hat nicht automatisch alle Rechte.
- **DC Empfehlungen**: Mindestens zwei DCs pro Domäne werden empfohlen.
- **RODC (Read Only Domain Controller)**: Bei einem RODC werden nicht alle Objekte repliziert.

#### Organisational Unit (OU)
- **Abbilden der Firmenstruktur**: z.B. Betrieb St. Gallen → IT Abteilung.
- **Verwaltungstätigkeiten**: Verwaltung der OU HR an Personalabteilung delegieren.
- **Gruppenrichtlinien**: Zuweisung von GPOs, z.B. Passwortrichtlinien.
- **Sichtbarkeit**: Nur Benutzer mit Leseberechtigung für die OU sehen deren Inhalt.

#### Unterschiedliche Sichtweisen
- **Logische Sicht**: Der Aufbau wirkt sich auf die Namensgebung und die Benutzerrechte aus.
- **Physische Sicht**: Die Replikation wird optimiert, ist für Benutzer unsichtbar.
