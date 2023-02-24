# Modul 169 - Services mit Containern bereitstellen

Lino Steffen

GLB Genossenschaft

Inf2021c

03.02.2023

Version 3.0



# Inhaltsverzeichnis

Tag 1 - Docker Grundlagen

Tag 2 - Docker Images

Tag 3 - Docker Compose

Tag 4 - Eigenes Projekt

Tag 5 -	Kubernetes

Tag 6 -  Kubernetes Deployments

Tag 7 -  Kubernetes Loadbalancer

Tag 8 -  Überwachung

Tag 9 -  Projekt

# Tag 1 - Docker Grundlagen

## Was sind Container und wo sind diese nützlich?

Container sind eine Form der virtuellen Isolation für Anwendungen und deren Abhängigkeiten. Sie ermöglichen es, Anwendungen unabhängig von der Hardware und dem Betriebssystem zu verpacken und zu transportieren. Dadurch können Anwendungen auf jedem System lauffähig sein, solange eine Container-Runtime bereitgestellt wird.

Ein Vorteil von Containern ist, dass sie es ermöglichen, Anwendungen in produktionsreifen Umgebungen einfach bereitzustellen, zu überwachen und zu skalieren. Ausserdem können sie dabei helfen, Konflikte zwischen Abhängigkeiten verschiedener Anwendungen zu vermeiden.

_Quelle: Internet + ich_

## Was ist DevOps?

DevOps ist eine Kultur, die eine enge Zusammenarbeit und Kommunikation zwischen Entwicklung und Betriebsteams fördert, um sicherzustellen, dass Anwendungen und Dienste schneller und zuverlässiger bereitgestellt werden können.

_Quelle: Internet_

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/HZIyS9czUHMAKMQOPczPCtS0.png)

## Unterschied Virtualisierung und Containerisierung

Virtualisierung und Containerisierung sind beide Technologien zur Isolation von Anwendungen und Abhängigkeiten, aber es gibt einige wichtige Unterschiede zwischen ihnen:

Die **Virtualisierung** nutzt eine virtuelle Maschine (VM), um ein vollständiges Betriebssystem und darauf laufende Anwendungen zu isolieren. Jede VM hat eigene Ressourcen.

Die **Containerisierung** nutzt einen Container, um nur die Anwendung und ihre Abhängigkeiten zu isolieren. Containers teilen sich das Betriebssystem des Hosts, wodurch sie weniger Ressourcen verbrauchen und schneller gestartet werden können als VMs. Containers sind für die Portabilität und Übertragbarkeit von Anwendungen ausgelegt und bieten eine höhere Effizienz als VMs.

_Quelle: Internet + ich_

## Unterschied Image und Container

Ein **Image** ist eine Vorlage für einen Container, die alle notwendigen Dateien und Einstellungen enthält, um eine Anwendung auszuführen. Es kann als «Abbild» einer vollständigen Umgebung für eine Anwendung angesehen werden. Ein Image kann als Vorlage für mehrere Container verwendet werden.

Ein Container ist eine isolierte Instanz einer Anwendung, die auf einem Host ausgeführt wird. Es nutzt das Betriebssystem des Hosts, aber ist durch eine isolierte Umgebung abgeschirmt, sodass es unabhängig von anderen Containern auf demselben Host ausgeführt werden kann. Jeder Container wird aus einem Image erstellt und kann eigene Einstellungen und Daten haben, die unabhängig von anderen Containern sind.

_Quelle: Internet + ich_

## Wichtigsten Befehle und ihre Funktion

| **Befehl** | **Funktion** |
| --- | --- |
| `sudo apt update` |  |
| `sudo apt upgrade` |  |
| `sudo apt install docker.io` | Docker installieren |
| `docker pull <service>` /<br>`docker pull ubuntu:21.10` /<br>`docker pull ubuntu:latest` | Lädt, Service runter<br>Ubuntu 21.10 herunterladen<br>Letzte Ubuntu Version herunterladen |
| `sudo docker images -a` | Image anzeigen |
| `sudo docker run <service>` | Docker Service starten |
| `docker run -it ubuntu bash` /<br>`docker run -it ubuntu:21.10 bash` | Bash aus dem Ubuntu starten<br>Bash aus dem Ubuntu 21.10 starten |
| `uname` | namen vom Betriebssystem |
| `ls` | list direcotry |
| `touch Lino-war-da` | erstellt eine Datei mit den Namen Lino war da |
| `exit` | verlassen |
| `hostname` | zeigt hostname an |
| `cat /etc/lsb-release` | Linux Version prüfen |
| `docker images` | heruntergeladene images anzeigen |
| `docker ps -a` | **Alle** Container auf meiner Kiste anzeigen |
| `docker ps` | laufende Conatainer anzeigen |
| `docker run --name <name> -d -p 8080:80 nginx` | **_--name some-nginx_** = Conatinername<br>**-d** dass es im Hintergrund laufen soll.<br>**-p 8080:80** verbindet den Host_port mit dem Container__port so dass eine Webanwendung via Browser von aussen erreichbar ist.<br>**nginx** dies sagt welches image gestartet werden soll, in unserem Fall nginx |
| `docker kill <ID> oder <name>` | Schnell, aber auf die harte Tour |
| `docker stop <ID> oder <name>` | Einzelnen Container sanft herunterfahren |
| `docker rm <ID> oder <name>` | Container löschen |
| `docker start <ID> oder <name>` | Container starten |
| `docker rmi nginx` | image löschen |
| `docker system prune -a --volumes` | Löscht alle **nicht** laufende Container |
| `docker logs <ID> oder <name>` | logs ansehen |
| docker logs  -f &lt;ID&gt; oder &lt;name&gt; | -f, sehen wir die Ausgabe laufend → auf Webseite zugreifen und dies wird im Log angezeigt |

## Onlyoffice

Onlyoffice installieren (ganzer Block eingeben)

```bash
sudo docker run --name onlyoffice -i -t -d -p 11012:80 \
-v /app/onlyoffice/DocumentServer/logs:/var/log/onlyoffice \
-v /app/onlyoffice/DocumentServer/data:/var/www/onlyoffice/Data onlyoffice/documentserver

```

The options:

-i := Keep STDIN open even if detached

-t := keep the container runtime alive

-d := the container is in the background in a “detached” mode

// -a := the container is in the foreground in a “attached” mode and can be connected to a STDIN,

STOUT, STERR

-p := Portmapping: The container is using Port 80, the Hostport is 11012

-v := Map directories from the Host into the container

Start test example

```bash
sudo docker exec 5a9cec2542cb sudo supervisorctl start ds:example

```

Add it to the autostart

```bash
sudo docker exec 5a9cec2542cb sudo sed 's,autostart=false,autostart=true,' -i /etc/supervisor/conf.d/ds-example.conf

```

→ Go to localhost on Port 11012

## Screenshot von Play, mit Docker eingeloggt

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/O0qTjAUN3-oNFPxsraRvmAyb.png)

## Screenshot OnlyOffice mit eigenem Namen und Datum im Dokument

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/kYC5hnCJS59cD9Z9QB3_DVVz.png)



# Tag 2 - Docker Images

## App Version 1

### Print Screen der Images bei GitLab

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/-kgH-_geyrXrT7OPagmyl_hO.png)

### Alle Befehle für «Ein Image Pushen» → App V1



**Wechsle ins Home Verzeichnis**

```
cd ~

```

**Clone git vom gitlab**

```
git clone git clone https://gitlab.com/thomas-staub/cloudmodules/m169/demobeispiele/to-do-appv1

```

**Im Ordner «web-fontend» todo-app image bauen**

```
docker image build -t todo-app:v1 .

```

**im Ordner «redis-slave» slave image bauen**

```
docker buils -t redis-slave:v1  .

```

**im Ordner «redis-master» master image bauen**

```
docker build -t redis-master:v1  .

```

**Gemeinsames Network erstellen**

```
docker network create todoapp_network

```

**docker run (master, slave, todo-app) version 1**

```
docker run --net=todoapp_network --name=redis-master -d redis-master:v1

```

```
docker run --net=todoapp_network --name=redis-slave -d redis-slave:v1

```

Wurde vorhin dies schon erstellt haben, das alte mit `docker rm -f frontend` entfernen.

```
docker run --net=todoapp_network --name=frontend -d -p 3000:3000 todo-app:v1

```

**Login Gitlab**

```
docker login gitlab.iet-gibb.ch:5050

```

**image tagen (master, slave, todo-app) version 1**

```
docker image tag redis-master:v1 gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-master:v1

```

```
docker image tag redis-slave:v1 gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-slave:v1

```

```
docker image tag redis-todo-app:v1 gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/todo-appv1:v1

```

**push (master, slave, todo-app) version 1**

```
docker push gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-master:v1

```

```
docker push gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-slave:v1

```

```
docker push gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/todo-app:v1

```

## App Version 2 Frontend

### Print Screen der Images bei GitLab

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/6Ys06SmMHkB8fg-nSLmkdJNi.png)

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/r7P2L8pFRctPhk0Pkta8gKDB.png)

### Alle Befehle für «Ein Image Pushen» → App V2

Zuvor das V1-frontent Image löschen → In Ordner `cd to-do-appv1/web-fontend/` wechseln. Und `docker rm -f frontend` anwenden.

**Im Home (**`cd ~`**)v2 git repository clonen**

```
git clone https://gitlab.com/thomas-staub/cloudmodules/m169/demobeispiele/to-do-appv2

```

**Im Ordner «web-fontend» das neue todo-app image bauen**

```
docker image build -t todo-app:v2  .

```

**neues Image starten _(Da wir vorher das alte schon gelöscht haben sollte dies kein Problem sein)_**

```
docker run --net=todoapp_network --name=frontend -d -p 3000:3000 todo-app:v2

```

**image tagen todo-app Version 2**

```
docker image tag todo-app:v2 gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv2/todo-app:v2

```

**push todo-app Version 2**

```
docker push gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv2/todo-app:v2

```



## Zusammenfassung der wichtigsten Befehle und Ihre Funktion



Docker Image erstellen

```
docker build .

```

Image tagen (mit repository name)

```
docker tag [imageid] [repositoryurl]

```

Image pushen

```
docker push [repositoryurl]

```

Docker komplett säubern

```
docker system prune  --all --volumes

```

Image von Repository pullen

```
docker pull [repositoryurl/imagename:tag]

```

# Tag 3 - Docker Compose

## Docker-Kommandoreferenz

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/yda2xX7u4PvZmKMt4SQp_CQH.png)

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/NI29BWL-bTQiXEvHshDfB2Qa.png)

## Was ist Docker Compose

Docker Compose ist ein Tool, das verwendet wird, um mehrere Docker-Container zusammen zu gruppieren und als eine Anwendung auszuführen. Mit Docker Compose kann man komplexe Anwendungen aus mehreren Containern definieren, die zusammenarbeiten müssen, und sie dann einfach mit einem einzigen Befehl starten, stoppen und verwalten. Dadurch wird die Verwaltung von Docker-Containern vereinfacht und automatisiert.

_Quelle: Internet + ich_

## Version 2 der App mit Docker Compose zum Laufen gebracht.

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/bb5bobNmHlnsqeCHtDZmDhGW.png)

### Vorgehen

1. docker compose installieren
1. Ordner und docker-compose.yml file erstellen
1. docker compose

### Befehle



**docker compose installieren**

Compose CLI-Plugin herunterzuladen und zu installieren

```
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

```

Ausführungsberechtigungen auf die Binärdatei anwenden

```
chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

```

Installation testen. - docker compose Version anzeigen.

```
docker compose version

```

Mehr Informationen unter: [https://docs.docker.com/compose/install/linux/#install-using-the-repository](https://docs.docker.com/compose/install/linux/#install-using-the-repository)



**docker compose up**

```yaml
docker compose -f docker-compose.yml up -d

```

**docker compose down**

```yaml
docker compose -f docker-compose.yml down

```



**Container log ansehen**

```yaml
docker logs <container id>

```

**Container live log ansehen**

```yaml
docker logs -f <container id> 

```

als Container-ID reichen die ersten Ziffern der ID



### To-do-List docker-compose.yml

Das Image wird von meinem gitlab genommen. Diese wo ich am 2. Tag erstellt habe.

```yaml
version: "1"
services:
  todoapp:
    image: gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv2/todo-app:v2
    ports:
      - "3000:3000"
    depends_on:
      - redis-master
      - redis-slave
  redis-slave:
    image: gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-slave:v1
    depends_on:
      - redis-master
  redis-master:
    image: gitlab.iet-gibb.ch:5050/lst135928/169/to-do-appv1/redis-master:v1

```

## Portainer installiert

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/WGbgoudkg6NwYQs_Km7f64u_.png)

w9Vu$YZ6!fzpegf

### Portainer docker-compose.yml

```yaml
# docker-compose.yaml 
version: '3'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./portainer-data:/data
    ports:
      - 9000:9000

```

### App via Portainer installiert und im Portfolio festgehalten

1. öffne portainer
1. local
1. Gehe zu «stacks» und «add stack»
1. name vergeben
1. docker-compose file einfügen
1. create

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/cBrNQfxhYfUIMoD-TMKDg8wN.png)

## Den Sock-Shop via Docker Compose installiert. 

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/8JnE_gGIZcydNn4BLMzQ3sB7.png)

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/5V1hKBLWv2Zr6Gi0-fTxx1pY.png)

### Vorgehen im Portfolio festgehalten. 

1. docker compose installiert
1. portainer installiert
1. git clone sock-shop
1. docker compose sock-shop



**clone git**

```yaml
git clone https://github.com/microservices-demo/microservices-demo

```

**In microservices-demo Ordner wechseln**

```yaml
cd microservices-demo

```

**docker compose**

```yaml
docker-compose -f deploy/docker-compose/docker-compose.yml up -d

```

_Quelle:_ [https://microservices-demo.github.io/deployment/docker-compose.html](https://microservices-demo.github.io/deployment/docker-compose.html)



**docker-compose.yml**

im Ordner ~/microservices-demo/deploy/docker-compose/docker-compose.yml

# Tag 4 - Eigenes Projekt

Ich habe eine Nginx Webserver erstellt.

Das Docker-compose File kann unter [https://github.com/LinoSteffen/Modul169](https://github.com/LinoSteffen/Modul169) heruntergeladen werden. Genauer wird dies jedoch im «Testversuch» unter diesem Beitrag beschrieben.

## Mein Vorgehen

### image erstellen und pushen

**Pull docker image**

```bash
docker image pull nginx:latest

```

**Ordner erstellen**

```bash
mkdir nginx-projects

```

**Im Ordner folgende Dateien erstellen**

```bash
touch Dockerfile && touch index.html

```

**Dockerfile**

```yaml
# Verwenden Sie das offizielle Nginx-Image als Basis
FROM nginx

# Kopieren Sie die HTML-Datei in den Container
COPY index.html /usr/share/nginx/html

# Ändern Sie den Besitzer und die Berechtigungen der HTML-Datei
RUN chown -R nginx:nginx /usr/share/nginx/html && chmod -R 755 /usr/share/nginx/html

# Exponieren Sie den Port 80, den Nginx verwendet
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

```

**index.html**

```xml
<!DOCTYPE html>
<html>
  <head>
    <title>linosteffen-test-webseite</title>
    <style>
      body {
        background-color: black;
        font-family: Arial, sans-serif;
      }
      h1 {
        font-size: 3em;
        text-align: center;
        color: white;
        margin-top: 70px;
      }
	   p {
        font-size: 1.3em;
        text-align: center;
        color: gray;
        margin-top: 30px;
      }
      h2 {
        font-size: 2em;
        text-align: center;
        color: white;
        margin-top: 70px;
      }
    </style>
  </head>
  <body>
    <div algin="center">
      <h1>Lino Steffen</h1>
      <p>This is a small test website</p>
      <h2>About</h2>
      <div style="text-align: center;">
        <img src="https://yt3.googleusercontent.com/HuPF5ereFLXCNbMrLwIJXUphhTUQFU8wJWK8fpA3niogik3STasG9zdH5NaBVyTw68uaTI-Q=s900-c-k-c0x00ffffff-no-rj" alt="Lino Steffen" style="width: 200px;">
      </div>      
      <p>Lino Steffen</br><a href="mailto:lst135928@stud.gibb.ch">lst135928@stud.gibb.ch</a>
      </p>
    </div>
  </body>
</html>

```

**Image erstellen**

```yaml
docker build -t linosteffen-nginx-project .

```

**login gitlab.iet-gibb.ch**

```
docker login gitlab.iet-gibb.ch:5050

```

**tag docker image**

```
docker image tag linosteffen-nginx-image:latest gitlab.iet-gibb.ch:5050/lst135928/169/linosteffen-nginx-image:v1

```

**push docker image**

```
docker push gitlab.iet-gibb.ch:5050/lst135928/169/linosteffen-nginx-image:v1

```

**docker-compose.yaml unter** [**https://github.com/LinoSteffen/Modul169**](https://github.com/LinoSteffen/Modul169) **erstellen**

```yaml
version: '1'

services:
  nginx:
    image: gitlab.iet-gibb.ch:5050/lst135928/169/linosteffen-nginx-image:v1
    ports:
      - 8000:80

```

### Testversuch

**git clonen**

```bash
git clone https://github.com/LinoSteffen/Modul169.git

```

**In Ordner wechseln**

```bash
cd Modul169

```

**docker compose**

```bash
docker-compose up -d

```

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/rad6xzuXVa381Rq-pUYPq_jM.png)

# Tag 5 -	Kubernetes

xx



# Tag 6 - Kubernetes Deployments

xx



# Tag 7 - Kubernetes Loadbalancer

xx



# Tag 8 - Überwachung

xx



# Tag 9 - Projekt

xx
