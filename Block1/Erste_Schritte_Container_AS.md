





2. Laden Sie das Image für den Apache Webserver (httpd:latest) herunter und starten Sie daraus einen 
   Container mit dem Kommando: 
   docker run -d --name my-apache-webserver -p 8080:80 httpd:latest 
   (-p 8080:80 bewirkt, dass der Server von localhost aus auf Port 8080 erreichbar ist)
   
   ```bash
   vmadmin@lp-22-04:~$ docker run -d --name my-apache-webserver -p 8080:80 httpd:latest
   Unable to find image 'httpd:latest' locally
   latest: Pulling from library/httpd
   8a1e25ce7c4f: Pull complete 
   8b0a7c8478f8: Pull complete 
   4f4fb700ef54: Pull complete 
   7f8fb0a042e0: Pull complete 
   91e4b2f2b52a: Pull complete 
   c78cdbf9617d: Pull complete 
   Digest: sha256:374766f5bc5977c9b72fdb8ae3ed05b7fc89060e7edc88fcbf142d6988e58eeb
   Status: Downloaded newer image for httpd:latest
   b2fa1c42632dfd466f0f31074292fe4246ba05ffa797d5edb0a23830a762af34
   
   ```

<img src="file:///C:/Users/Abel%20Solomon%20(Schule/AppData/Roaming/marktext/images/2024-04-02-11-25-42-image.png" title="" alt="" width="367">

Der Server läuft

Starten Sie eine interaktive bash-Sitzung (-it) im Container und finden Sie heraus, wo sich die 
angezeigte Seite index.html im Container befindet. Die Sitzung können Sie mit exit wieder verlassen 


`docker exec -it my-apache-webserver /bin/bash`



```bash
vmadmin@lp-22-04:~$ docker exec -it my-apache-webserver /bin/bash
//Ausgabe
root@b2fa1c42632d:/usr/local/apache2# 


```

Starten Sie aus dem Image httpd:latest einen zweiten Container auf Port 8081

```bash
vmadmin@lp-22-04:~$ docker run -d --name my-apache-webserver2 -p 8081:80 httpd:latest
41d8c86bc62cdf64f9c592e572bafb2e81f2b603ee45318b82b99381a19d8711

```

Lassen Sie sich die laufenden Container anzeigen

```bash
vmadmin@lp-22-04:~$ docker ps -a
CONTAINER ID   IMAGE                           COMMAND              CREATED              STATUS                      PORTS                                                           NAMES
41d8c86bc62c   httpd:latest                    "httpd-foreground"   About a minute ago   Up About a minute           0.0.0.0:8081->80/tcp, :::8081->80/tcp                           my-apache-webserver2
b2fa1c42632d   httpd:latest                    "httpd-foreground"   7 minutes ago        Up 6 minutes                0.0.0.0:8080->80/tcp, :::8080->80/tcp                           my-apache-webserver
0d3affb065e7   hello-world                     "/hello"             56 minutes ago       Exited (0) 56 minutes ago                                                                   agitated_lovelace
2cd9b983b1db   portainer/portainer-ce:latest   "/portainer"         15 months ago        Up About an hour            8000/tcp, 9000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer

```

Lassen Sie sich alle Images anzeigen

```bash
vmadmin@lp-22-04:~$ docker images
REPOSITORY               TAG       IMAGE ID       CREATED         SIZE
httpd                    latest    ac45b24b92cc   2 months ago    167MB
hello-world              latest    d2c94e258dcb   11 months ago   13.3kB
portainer/portainer-ce   latest    5f11582196a4   16 months ago   287MB

```

Stoppen Sie einen der Container

```bash
vmadmin@lp-22-04:~$ docker stop b2fa1c42632d //ID ist von dem jeweiligen Container
b2fa1c42632d


```

Lassen Sie sich die laufenden und gestoppten Container anzeigen

```bash
vmadmin@lp-22-04:~$ docker ps -a

CONTAINER ID   IMAGE                           COMMAND              CREATED          STATUS                          PORTS                                                           NAMES
41d8c86bc62c   httpd:latest                    "httpd-foreground"   4 minutes ago    Up 4 minutes                    0.0.0.0:8081->80/tcp, :::8081->80/tcp                           my-apache-webserver2
b2fa1c42632d   httpd:latest                    "httpd-foreground"   10 minutes ago   Exited (0) About a minute ago                                                                   my-apache-webserver
0d3affb065e7   hello-world                     "/hello"             59 minutes ago   Exited (0) 59 minutes ago                                                                       agitated_lovelace
2cd9b983b1db   portainer/portainer-ce:latest   "/portainer"         15 months ago    Up About an hour                8000/tcp, 9000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer

```

Starten Sie den gestoppten Container wieder 



```bash
vmadmin@lp-22-04:~$ docker start b2fa1c42632d //ID des Containers
b2fa1c42632d


```

Löschen Sie alle Container ausser Portainer

```bash
//Zuerst müssen alle laufenden Container gestoppt werden

vmadmin@lp-22-04:~$ docker stop 41d8c86bc62c
41d8c86bc62c
vmadmin@lp-22-04:~$ docker stop b2fa1c42632d
b2fa1c42632d 

//Jetzt können Sie gelöscht werden 

madmin@lp-22-04:~$ docker rm my-apache-webserver2
my-apache-webserver2
vmadmin@lp-22-04:~$ docker rm my-apache-webserver
my-apache-webserver 

//Überprüfung
vmadmin@lp-22-04:~$ docker ps -a
CONTAINER ID   IMAGE                           COMMAND        CREATED         STATUS             PORTS                                                           NAMES
2cd9b983b1db   portainer/portainer-ce:latest   "/portainer"   15 months ago   Up About an hour   8000/tcp, 9000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer

```

Löschen Sie alle Images (ausser Portainer) 

```bash
vmadmin@lp-22-04:~$ docker rmi httpd
Untagged: httpd:latest
Untagged: httpd@sha256:374766f5bc5977c9b72fdb8ae3ed05b7fc89060e7edc88fcbf142d6988e58eeb
Deleted: sha256:ac45b24b92cc0527c6af660679d0701f680a6d4214cf5cf9a147f20127d9685e
Deleted: sha256:f05921eb27f3a6477b22284fcb69a1d5be244dd94ddee40700014305c6e7b8f3
Deleted: sha256:6721078d05153c2ea23c831c8b87d437177abca9edafe43f7fcdb405a8ac8430
Deleted: sha256:7c89dd89a4101d1bb42d0eb9d9cf145906c4e574826c3792f7211325362e563a
Deleted: sha256:34fa6dddb40afdba66482396f5e08ad22f646fb4fc9770e5d02dd4c61c18db00
Deleted: sha256:25c712dda17c439dc446a448c708596dbda15aa42f88e99685eda1b25d30b2c0
Deleted: sha256:a483da8ab3e941547542718cacd3258c6c705a63e94183c837c9bc44eb608999 

vmadmin@lp-22-04:~$ docker rmi hello-world
Untagged: hello-world:latest
Untagged: hello-world@sha256:53641cd209a4fecfc68e21a99871ce8c6920b2e7502df0a20671c6fccc73a7c6
Deleted: sha256:d2c94e258dcb3c5ac2798d32e1249e42ef01cba4841c2234249495f87264ac5a
Deleted: sha256:ac28800ec8bb38d5c35b49d45a6ac4777544941199075dff8c4eb63e093aa81e



```


