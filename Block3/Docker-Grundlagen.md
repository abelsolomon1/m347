### Containerisierung:

- **Definition**: Containerisierung ist eine Methode zur Bereitstellung und Ausführung von Anwendungen in isolierten Umgebungen, genannt Container.
- **Vorteile**: Isolierung, Portabilität, Skalierbarkeit, Effizienz.
- **Beispiel**: Ein Container für eine Webanwendung enthält alle notwendigen Bibliotheken, Abhängigkeiten und Einstellungen, um die Anwendung auf jedem System auszuführen, unabhängig von der Umgebung.

### Docker:

- **Definition**: Docker ist eine Open-Source-Plattform zur Automatisierung von Container-Bereitstellung, -Management und -Skalierung.
- **Bestandteile**: Docker Engine, Docker Images, Docker Container.
- **Beispiel**: `docker run hello-world` lädt das "hello-world" Image von Docker Hub herunter und startet einen Container, der eine einfache Ausgabe zeigt.

### Virtualisierung vs. Containerisierung:

- **Unterschiede**: Bei der Virtualisierung wird eine vollständige virtuelle Maschine erstellt, die ein eigenes Betriebssystem enthält. Bei der Containerisierung teilen sich Container den Kernel des Host-Betriebssystems.
- **Beispiel**: Virtualisierung: VMware, VirtualBox. Containerisierung: Docker, Kubernetes.

## Docker-Grundlagen

### Docker Commands:

- `docker create`: Erzeugt ein neues Container-Image.
- `docker start`: Startet einen oder mehrere gestoppte Container.
- `docker stop`: Stoppt einen oder mehrere laufende Container.
- `docker rm`: Löscht einen oder mehrere gestoppte Container.
- **Beispiel**: `docker create my-container-image`

### Docker Run Options:

- `--name`: Gibt dem Container einen Namen.
- `--rm`: Entfernt den Container nach dem Beenden.
- `-d`: Führt den Container im Hintergrund aus.
- `-it`: Interaktiver Modus.
- `-p`: Portweiterleitung.
- `-v`: Volumenmontage.
- `-e`: Umgebungsvariablen.
- **Beispiel**: `docker run --name my-container -d -p 8080:80 my-image`

### Dockerfile:

- **Definition**: Ein Dockerfile ist eine Textdatei, die eine Reihe von Anweisungen enthält, um ein Docker-Image zu erstellen.
- **Anweisungen**: FROM, RUN, COPY, ADD, CMD, ENTRYPOINT, ENV, EXPOSE, VOLUME, WORKDIR, USER, LABEL.
- **Beispiel**:



```bash
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]

```

### Image Tags und Versionierung:

- **Definition**: Docker-Images können mit Tags versehen werden, um verschiedene Versionen zu kennzeichnen.
- **Beispiel**: `docker pull nginx:latest`, `docker pull nginx:1.19.10`

### Portweiterleitungen und Volumenmontage:

- **Portweiterleitung**: Erlaubt den Zugriff auf Ports innerhalb des Containers von außen.
- **Volumenmontage**: Ermöglicht den Zugriff auf Dateien und Ordner außerhalb des Containers.
- **Beispiel**: `docker run -d -p 8080:80 -v /host/path:/container/path my-image`

## Docker-Netzwerke

- **Definition**: Docker ermöglicht die Definition von Netzwerken, die Containern zugewiesen werden können, um die Kommunikation zu ermöglichen.
- **Beispiel**: `docker network create my-network`v 
