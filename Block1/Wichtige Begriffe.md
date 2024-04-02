# Docker Glossar

## Docker Image

Ein Docker Image ist eine Vorlage, die alle Bestandteile einer Anwendung enthält.

## Dockerfile

Ein Dockerfile ist eine Textdatei mit Anweisungen zum Erstellen eines Docker Images.

## Docker Container

Ein Docker Container ist eine Laufzeitinstanz eines Docker Images, die isoliert und portabel ist.

## Docker Registry

Ein Docker Registry ist ein zentraler Speicherort für Docker Images, z.B. Docker Hub.





# Virtuelle Maschine

- Läuft auf einem Hypervisor, einer Emulationssoftware zwischen Hardware und VM.
- Jede VM hat ihr eigenes Gastbetriebssystem.
- Benötigt mehr Ressourcen und ist weniger agil als Container.
- Der Hypervisor verwaltet die gemeinsame Nutzung physischer Ressourcen.

# Container

- Befindet sich auf einem physischen Server und teilt sich das Host-Betriebssystem.
- Teilt sich ein gemeinsames Betriebssystem, was für Fehlerbehebungen und Patches sorgt.
- Ist agiler und hat eine höhere Portabilität als virtuelle Maschinen.
- Läuft in der Regel in einem leichtgewichtigen, isolierten Prozess.
