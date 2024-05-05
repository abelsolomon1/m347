---

# Dockerfile Schlüsselwörter

Hier sind die Schlüsselwörter, die im Dockerfile verwendet werden, und ihre Bedeutungen mit Beispielen:

### ADD

Kopiert Dateien vom Host oder einer entfernten URL in das Dateisystem des Images.

Beispiel:

```bash
ADD ./app.jar /usr/local/bin/app.jar
```

### CMD

Setzt das Kommando, das beim Start des Containers ausgeführt wird, sofern es nicht übersteuert wird.

Beispiel:

```bash
CMD ["java", "-jar", "/usr/local/bin/app.jar"]
```

### COPY

Kopiert Dateien vom Host in das Dateisystem des Images.

Beispiel:

```bash
COPY ./app.jar /usr/local/bin/app.jar
```

### ENTRYPOINT

Setzt das Kommando, das beim Start des Containers immer ausgeführt wird.

Beispiel:

```bash
ENTRYPOINT ["java", "-jar", "/usr/local/bin/app.jar"]
```

### ENV

Setzt eine Umgebungsvariable.

Beispiel:

```bash
ENV APP_HOME /usr/local/bin
```

### EXPOSE

Definiert die zur Laufzeit des Containers aktiven Netzwerk-Ports.

Beispiel:

`EXPOSE 8080`

### FROM

Setzt das Basis-Image für die nachfolgenden Anweisungen.

Beispiel:

`FROM openjdk:11-jre`

### LABEL

Fügt dem Image Metadaten hinzu.

Beispiel:

`LABEL maintainer="example@example.com"`

### RUN

Führt das angegebene Kommando einmalig während docker build aus und erzeugt dadurch einen neuen Image-Layer.

Beispiel:

`RUN apt-get update && apt-get install -y curl`

### USER

Gibt den Account für RUN, CMD und ENTRYPOINT an.

Beispiel:

`USER appuser`

### VOLUME

Definiert einen Mount Point auf ein Verzeichnis auf dem Host oder einem anderen Container.

Beispiel:

`VOLUME /var/log/app`

### WORKDIR

Legt das Arbeitsverzeichnis für RUN, CMD, COPY etc. fest.

Beispiel:

`WORKDIR /usr/local/bin`
