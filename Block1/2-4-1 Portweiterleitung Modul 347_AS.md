## 2.4-1 Portweiterleitung Modul 347

© 2023 gbssg.ch | Informatik | M347  1 

### Ziele

1. Sie erkennen welchen Zusammenhang zwischen internem Containerport und externem Hostport besteht. 

### Aufgaben

Suchen Sie in Docker Hub nach dem Image "getting-started". Getting-started bietet eine Webseite mit elementaren Informationen zu Docker an. Lösen Sie folgende Aufgaben:

1. **Auf welchem Port läuft die Webseite im Container?**
   
   Der Container läuft auf dem Port 80:80
   
   ![](C:\Users\Abel%20Solomon%20(Schule\AppData\Roaming\marktext\images\2024-04-07-20-48-52-image.png)

2. **Starten Sie einen Container aus getting-started, der auf dem Host auf http://localhost:8080 erreichbar ist.**
   
   ```bash
   docker run -d --name AbelsContainer -p 8080:80 docker/getting-started:latest 
   
   #Ausgabe
   
   Unable to find image 'docker/getting-started:latest' locally
   latest: Pulling from docker/getting-started
   c158987b0551: Pull complete 
   1e35f6679fab: Pull complete 
   cb9626c74200: Pull complete 
   b6334b6ace34: Pull complete 
   f1d1c9928c82: Pull complete 
   9b6f639ec6ea: Pull complete 
   ee68d3549ec8: Pull complete 
   33e0cbbb4673: Pull complete 
   4f7e34c2de10: Pull complete 
   Digest: sha256:d79336f4812b6547a53e735480dde67f8f8f7071b414fbd9297609ffb989abc1
   Status: Downloaded newer image for docker/getting-started:latest
   0c8d37a2d7d33fcf3152caa85b081ea8e2c7490aeaad6bbf3c12aeafdca1fda7
   ```
   
   ![](C:\Users\Abel%20Solomon%20(Schule\AppData\Roaming\marktext\images\2024-04-07-21-50-22-image.png)

3. **Worin könnte eine Problematik bei der Integration in ein lokales Netzwerk auftreten? Denken Sie dabei an den Fall, bei dem Sie bereits einen lokalen Webserver laufen haben.**

        Es können Probleme auftreten wenn vielleicht eine anderer Host auf dem Port         8080 verwendet wird. Dies kann zu Konflikten führen. Da ich aber keinen         laufenden

4. **Beantworten Sie die Frage: Warum funktioniert `docker run -d --name my-apache webserver -p 8080:80 httpd:latest` aus Aufgabe 2.3.1 nicht mehr?**

        Da der Container bereits erstellt bzw. heruntergeladen wurde, entsteht ein         Konflikt. Dieser Konflikt kann gelöst werden indem man diesen Container entfernt         oder den Namen des Containers ändert.  

```bash
#Fehlermeldung
vmadmin@lp-22-04:~$ docker run -d --name my-apache-webserver -p 8080:80 httpd:latest
docker: Error response from daemon:
Conflict. 
The container name "/my-apache-webserver" is already in use by container "e16322a596fcafa6bdeb52df82c3fbf841b8afb2cfc93ce5b717668cd1d8bb15". 
You have to remove (or rename) that container to be able to reuse that name.
```

![](C:\Users\Abel%20Solomon%20(Schule\AppData\Roaming\marktext\images\2024-04-07-21-42-41-image.png) 

5. **Lesen Sie getting-started durch**
   
   Grundlegende Konzepte wie Container, Images und Dockerfiles
   
   Erstellen und Ausführen von Containern
   
   Arbeiten mit Dockerfiles zur Erstellung benutzerdefinierter Images
   
   Netzwerk-Konfiguration, einschliesslich Portweiterleitung
   
   Verwaltung von Images und Containern mit grundlegenden Docker-Befehlen

6. **Beenden Sie am Schluss den Container, löschen Sie ihn und auch das Image.**
   
   ```bash
   #Auflistung der Container
   vmadmin@lp-22-04:~$ docker ps -a
   CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                                           NAMES
   0c8d37a2d7d3   docker/getting-started:latest   "/docker-entrypoint.…"   31 minutes ago   Up 31 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp                           AbelsContainer
   e16322a596fc   httpd:latest                    "httpd-foreground"       5 days ago       Created                                                                         my-apache-webserver
   2cd9b983b1db   portainer/portainer-ce:latest   "/portainer"             15 months ago    Up 2 hours      8000/tcp, 9000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer 
   ```

```
     Jetzt kopiere ich die Container ID von getting-started und stoppe ihn:

```bash
vmadmin@lp-22-04:~$ docker stop 0c8d37a2d7d3
0c8d37a2d7d3
```

        Nun muss ich den Container löschen:

```bash
vmadmin@lp-22-04:~$ docker rm  0c8d37a2d7d3
0c8d37a2d7d3
```

         Zum Schluss lösche ich das Image

```bash
#Beachte, dass die ID des Image ein anderes ist als der des Containers.
vmadmin@lp-22-04:~$ docker rmi 3e4394f6b72f
Untagged: docker/getting-started:latest
Untagged: docker/getting-started@sha256:d79336f4812b6547a53e735480dde67f8f8f7071b414fbd9297609ffb989abc1
Deleted: sha256:3e4394f6b72fccefa2217067a7f7ff84d5d828afa9623867d68fce4f9d862b6c
Deleted: sha256:cdc6440a971be2985ce94c7e2e0c2df763b58a2ced4ecdb944fcd9b13e7a2aa4
Deleted: sha256:041ac26cd02fa81c8fd73cc616bdeee180de3fd68a649ed1c0339a84cdf7a7c3
Deleted: sha256:376baf7ada4b52ef4c110a023fe7185c4c2c090fa24a5cbd746066333ce3bc46
Deleted: sha256:d254c9b1e23bad05f5cde233b5e91153a0540fa9a797a580d8a360ad12bf63a9
Deleted: sha256:dd5c79fa9b6829fd08ff9943fc1d66bebba3e04246ba394d57c28827fed95af0
Deleted: sha256:8d812a075abf60a83013c37f49058c220c9cdf390266952126e7e60041b305dc
Deleted: sha256:ff1787ee3dcae843dc7dd1933c49350fc84451cf19ed74f4ea72426e17ee7cd1
Deleted: sha256:85ebd294be1553b207ba9120676f4fd140842348ddf1bb5f7602c7a8401f0a13
Deleted: sha256:ded7a220bb058e28ee3254fbba04ca90b679070424424761a53a043b93b612bf
```

![](C:\Users\Abel%20Solomon%20(Schule\AppData\Roaming\marktext\images\2024-04-07-21-38-38-image.png)

### Erwartete Resultate

Mit Screenshots dokumentiertes und kommentiertes Vorgehen. 
Zeit: 30 Minuten
