╔══════════════════════════════════════════════════╗
║  All ye who enter here,                          ║
║        abandon all hope.                         ║
╚══════════════════════════════════════════════════╝


# Docker Wochenprojekt – IT-Infrastruktur

Dieses Projekt stellt eine containerisierte IT-Infrastruktur mit Docker Compose bereit.
Alle Dienste werden automatisiert gestartet, sodass nach einem einmaligen
`docker compose up -d` kein weiterer manueller Eingriff erforderlich ist.

## Projektziel

Ziel des Projekts ist der Aufbau einer reproduzierbaren Serverumgebung mit:
- Cloud-Dienst
- Reverse Proxy
- Monitoring
- Backup-System
- Dashboard / Landingpage
- optionalem Bonusdienst

Die Umgebung ist so aufgebaut, dass sie auf einem beliebigen Docker-Host
denselben funktionsfähigen Zustand erreicht.

---

## Projektstruktur

Der Projektordner muss folgende Struktur besitzen:

docker-projekt/
├─ docker-compose.yml
├─ Caddyfile
├─ homepage/
│ └─ config/
│ ├─ services.yaml
│ └─ settings.yaml
├─ monitoring/
│ └─ prometheus/
│ └─ prometheus.yml
└─ README.md


**Wichtig:**  
Datenverzeichnisse (z. B. Nextcloud-Daten, Backups, Datenbanken) werden
automatisch als Docker-Volumes erstellt und sind **nicht Teil der Abgabe**.

---

## Start der Umgebung

### Voraussetzungen
- Docker
- Docker Compose (Plugin oder Standalone)

### Start

docker compose up -d

Nach dem Starten stehen alle Dienste automatisch zur Verfügung.

Enthaltene Dienste
1. Reverse Proxy (Caddy)

Zentrale Zugriffsstelle für Webdienste

Weiterleitung der Anfragen an die internen Container

Umsetzung eines Reverse-Proxy-Konzepts gemäß Anforderung

2. Nextcloud (Cloud-Dienst)

Dateiablage und Kollaboration

Zugriff über:
http://10.145.240.109

3. Dashboard / Landingpage (Homepage)

Übersicht aller bereitgestellten Dienste

Zugriff über:
http://10.145.240.109/dashboard

4. Monitoring

Prometheus sammelt Metriken

Grafana visualisiert diese Metriken

Zugriff auf Grafana:
http://10.145.240.109:1337

5. Backup-System

FTP-Server zur Ablage von Backups

Automatisches Backup der Nextcloud-Daten

Backups werden regelmäßig ohne Benutzerinteraktion erstellt

6. Wiki.js (Bonusdienst)

Dokumentations- und Wissensplattform

Zugriff über:
http://10.145.240.109:3001

Hinweis zur Architektur:
Eine Einbindung von Wiki.js über einen URL-Unterpfad wurde evaluiert,
jedoch aufgrund fehlender stabiler Subpath-Unterstützung der Anwendung
bewusst verworfen.
Der Dienst wird daher über einen dedizierten Port bereitgestellt.

| Dienst    | Adresse / Port                                                     |
| --------- | ------------------------------------------------------------------ |
| Nextcloud | [http://10.145.240.109](http://10.145.240.109)                     |
| Dashboard | [http://10.145.240.109/dashboard](http://10.145.240.109/dashboard) |
| Grafana   | [http://10.145.240.109:1337](http://10.145.240.109:1337)           |
| Wiki.js   | [http://10.145.240.109:3001](http://10.145.240.109:3001)           |
| FTP       | (Port 21)                                                          |


Reproduzierbarkeit

Das Projekt ist vollständig reproduzierbar:

Alle Dienste werden über docker-compose.yml definiert

Alle benötigten Konfigurationsdateien liegen im Projektordner

Kein manuelles Nachkonfigurieren nach dem Start notwendig

Nach dem Kopieren des Projektordners und Ausführen von

docker compose up -d

