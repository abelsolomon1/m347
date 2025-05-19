
# Docker Spickzettel – Praktische Prüfung (Bestnote-Edition)

**Hinweis:** Internet erlaubt, aber keine KI. Dieser Spick ist so gebaut, dass du dich auch ohne viel Übung sicher zurechtfindest!

---

## 1. Grundbegriffe (Kurz & Wichtig)

- **Image**: Vorlage für Container mit App & Umgebung (schreibgeschützt)
- **Container**: Laufende, isolierte Instanz eines Images (leichtgewichtig)
- **Dockerfile**: Anleitung zum Bauen eines Images (Textdatei)
- **Registry**: Ort zum Speichern und Laden von Images (z. B. Docker Hub)
- **Repository**: Sammlung von Images mit Versionen (Tags)
- **Volume**: Speicher für persistente Daten (außerhalb des Containers)
- **Netzwerk**: Verbindung zwischen Containern (Standard: `bridge`)
- **Docker Engine**: Besteht aus Daemon (Server) & CLI (Client)

---

## 2. Wichtige CLI-Befehle

```bash
docker run [OPTIONEN] IMAGE [COMMAND]
```

### Beispiel:
```bash
docker run -d --name web -p 8080:80 nginx
```

### Optionen
| Option       | Erklärung                             |
|--------------|----------------------------------------|
| `--name`     | Container benennen                     |
| `--rm`       | Löscht Container nach Beenden          |
| `-d`         | Start im Hintergrund                   |
| `-it`        | Interaktiver Terminal                  |
| `-p H:C`     | Portweiterleitung Host:Container       |
| `-v Q:Z`     | Volume mounten                         |
| `-e`         | Umgebungsvariable setzen               |
| `--network`  | Netzwerk zuweisen                      |
| `--ip`       | IP-Adresse im Netzwerk setzen          |

---

## 3. Container & Images verwalten

```bash
docker pull IMAGE[:TAG]       # Image laden
docker build -t name .        # Image bauen
docker images                 # Lokale Images anzeigen
docker ps -a                  # Alle Container anzeigen
docker stop CONTAINER         # Container stoppen
docker rm CONTAINER           # Container löschen
docker rmi IMAGE              # Image löschen
```

---

## 4. Dockerfile Basics

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

### Wichtigste Anweisungen

| Befehl      | Bedeutung                                           |
|-------------|-----------------------------------------------------|
| `FROM`      | Basis-Image setzen                                  |
| `COPY`      | Dateien vom Host ins Image kopieren                |
| `ADD`       | Wie COPY, kann aber auch URLs & `.tar` entpacken   |
| `RUN`       | Befehle beim Build ausführen                        |
| `CMD`       | Startkommando (überschreibbar)                     |
| `ENTRYPOINT`| Startkommando (nicht überschreibbar)               |
| `ENV`       | Umgebungsvariable setzen                            |
| `EXPOSE`    | Dokumentiert offenen Port                           |
| `VOLUME`    | Mount-Point für externe Daten                       |
| `WORKDIR`   | Arbeitsverzeichnis setzen                           |
| `USER`      | Benutzer für nachfolgende Befehle                   |
| `LABEL`     | Metadaten hinzufügen                                |

---

## 5. Netzwerke

```bash
docker network create   --driver bridge   --subnet 192.168.100.0/24   my-net
```

```bash
docker run -d --name myapp   --network my-net   --ip 192.168.100.10   nginx
```

---

## 6. Volumes

### Benanntes Volume
```bash
docker volume create daten-vol
docker run -d --name c1 -v daten-vol:/app alpine sleep 1000
```

### Bind-Mount (lokales Verzeichnis):
```bash
docker run -d   -v $(pwd)/html:/usr/share/nginx/html   -p 8080:80   nginx
```

---

## 7. Schritt-für-Schritt: Portweiterleitung

**Ziel:** Container über Port auf dem Host erreichen (z. B. Webserver)

```bash
docker run -d   --name web   -p 8080:80   nginx
```

- `-p 8080:80`: Leitet Host-Port 8080 auf Container-Port 80
- `-d`: Im Hintergrund starten
- Test: `curl http://localhost:8080` oder im Browser

---

## 8. Schritt-für-Schritt: Volume-Nutzung

### A) Benanntes Volume
```bash
docker volume create daten-vol
docker run -d --name c1 -v daten-vol:/data alpine sleep 1000
docker exec -it c1 sh
echo "Hallo" > /data/datei.txt
```

### B) Lokaler Bind-Mount
```bash
mkdir html
echo "<h1>Test</h1>" > html/index.html

docker run -d   --name nginx-html   -v $(pwd)/html:/usr/share/nginx/html   -p 8080:80   nginx
```

Test: `curl http://localhost:8080`

---

## 9. Mehrere Image-Versionen

```bash
docker pull alpine            # neueste Version
docker pull alpine:3.18       # bestimmte Version
docker run -it --rm alpine:3.18 sh
```

---

## 10. Debug & Prüfung

```bash
docker exec -it CONTAINER sh     # In Container einloggen
docker logs CONTAINER            # Logs anzeigen
docker inspect CONTAINER         # Details prüfen
curl localhost:PORT              # Verbindung testen
```

---

## 11. CMD vs. ENTRYPOINT

| CMD            | ENTRYPOINT                        |
|----------------|-----------------------------------|
| Überschreibbar | Bleibt fix                        |
| Gut für Standardbefehle | Gut für feste Startlogik  |

---

## 12. COPY vs. ADD

| COPY         | ADD                                      |
|--------------|-------------------------------------------|
| Nur lokale Dateien | Kann auch URLs und `.tar` entpacken |

---

## 13. Vergleich: Container vs. VM

| Container                         | VM                                |
|----------------------------------|-----------------------------------|
| Startet in Sekunden              | Startet in Minuten                |
| Teilt Kernel mit Host            | Eigener Kernel                    |
| Weniger Overhead                 | Mehr Ressourcen nötig             |
| Schnell & leichtgewichtig        | Schwer & isolierter               |

---

## 14. Häufige Fehler & Lösungen

| Problem                       | Lösung                              |
|------------------------------|-------------------------------------|
| Port nicht erreichbar        | `-p` vergessen? Port korrekt?       |
| Datei fehlt im Container     | `COPY` oder `-v` prüfen             |
| Container stoppt sofort      | CMD falsch? Interaktiv starten      |
| Image zu groß                | `RUN`-Anweisungen zusammenfassen    |

---

## 15. Schnell-Anleitungen

### Eigene Web-App (Node.js o. ä.)
```bash
docker build -t webapp .
docker run -d -p 3000:3000 webapp
```

### HTML mit NGINX anzeigen
```bash
docker run -d   --name web   -p 8080:80   -v $(pwd)/html:/usr/share/nginx/html   nginx
```

---

**Letzter Tipp:**  
Arbeite ruhig, teste immer mit `docker ps`, `docker logs`, `curl` und `docker exec`.

**Viel Erfolg – du hast alles Wichtige dabei!**
