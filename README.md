# SnowStreamCDN

SnowStreamCDN ist ein selbst betriebenes Content Delivery Network (CDN) für Livestreams von Snowgames.live. Ziel ist es, Livestreams unabhängig von Plattformen wie YouTube mit geringer Latenz, hoher Stabilität und Hosting in Europa und Nordamerika bereitzustellen.

## 🎯 Ziel

Das Projekt bietet eine flexible, skalierbare und redundante Streamingarchitektur für Sportevents. Zuschauer erhalten Streams direkt von unseren eigenen Servern, die Last wird über DNS und Loadbalancer verteilt.

## 🏗️ Architektur

- **Encoder**:  
  - OBS Studio (primär)  
  - mediamtx als optionaler Ingest-Server lokal auf dem OBS-Rechner

- **Zentrale Verteilung**:  
  - OBS streamt per RTMP/SRT an zwei redundante Datarhei Restreamer
  - Restreamer pushen den Stream an zwei mediamtx-Server
  - mediamtx erzeugt HLS-Chunks und Playlists (.m3u8)

- **Content Delivery**:  
  - Mehrere Webserver ziehen die HLS-Chunks per HTTP von den mediamtx-Servern
  - Loadbalancer und DNS sorgen für Ausfallsicherheit und Lastverteilung auf Entry-VPS

## 📡 Encoder- und Kamera-Setup

- Zowitek-Boxen als HDMI-zu-SRT/NDI-Encoder an Spielstätten
- DJI Pocket 3 / DJI Action 4 Kameras integriert
- Zowitek-Boxen dienen auch als Decoder im Studio (HDMI-Ausgabe für den Bildmischer)

## 🔧 Netzwerk & Bandbreite

- Bondix bündelt DSL, LTE Vodafone GigaCubes, Starlink für stabile Uploads ≥10 Mbit/s pro Stream
- VLAN-Setup mit Unifi/Omada-Komponenten zur Trennung von Kameras, Encoder und Streamingservern (eigenes Event WLAN)

## ⚙️ Technische Details

- mediamtx wird mit JSON-Konfiguration betrieben, Streams werden per API abgefragt
- Restreamer (Datarhei) stellt zentrale Distribution sicher
- Nginx-Webserver liefern ausschließlich statische HLS-Dateien aus
- Entry-VPS mit eigenen DNS-Servern (PowerDNS/CoreDNS) verteilen den Traffic

## 🛠️ Status

✅ Streaming-Pipeline steht konzeptionell (OBS → Restreamer → mediamtx → Webserver)  
✅ ffmpeg-Testpattern erfolgreich getestet  
✅ Zowitek-Encoder/Decoder integriert  
🛠️ Webserver-Setup in Arbeit  
🛠️ Monitoring und API-Automatisierung in Vorbereitung

## 📑 Herausforderungen

- Synchronisierung mehrerer Kamerastreams mit niedriger Latenz
- Integration von PTZ-Kameras mit eingeschränkter Steuerung (z. B. HDKatov, PTZoptiks)
- Aufbau von DNS- und Entry-VPS-Infrastruktur für Redundanz und Failover

## 🚀 Zielgruppe

- Eigene Sportevents (z. B. Biathlon, Mountainbike, Tischtennis, Fußball, Skilanglauf, Blindensport - Showdown, Triathlon)
- Zuschauer, die Streams direkt auf unserer Webseite abrufen sollen
- Partner, die Streaminginhalte in hoher Qualität und Zuverlässigkeit benötigen

---

**SnowStreamCDN** – Eine unabhängige, stabile Streaminglösung für Snowgames.live!
