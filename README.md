**Modul 169**

Lino Steffen

GLB Genossenschaft

Inf2021c

03.02.2023

Version 1.0



# Inhaltsverzeichnis

Tag 1 - Container Grundlagen

Tag 2 - Befehle und Funktionen

Tag 3 -

Tag 4 -

Tag 5 -

Tag 6 -

Tag 7 -

Tag 8 -

Tag 9 -

# Tag 1 - Container Grundlagen

## Was sind Container und wo sind diese nützlich?

Container sind eine Form der virtuellen Isolation für Anwendungen und deren Abhängigkeiten. Sie ermöglichen es, Anwendungen unabhängig von der Hardware und dem Betriebssystem zu verpacken und zu transportieren. Dadurch können Anwendungen auf jedem System lauffähig sein, solange eine Container-Runtime bereitgestellt wird.

Ein Vorteil von Containern ist, dass sie es ermöglichen, Anwendungen in produktionsreifen Umgebungen einfach bereitzustellen, zu überwachen und zu skalieren. Ausserdem können sie dabei helfen, Konflikte zwischen Abhängigkeiten verschiedener Anwendungen zu vermeiden.



## Was ist DevOps?

DevOps ist eine Kultur, die eine enge Zusammenarbeit und Kommunikation zwischen Entwicklung und Betriebsteams fördert, um sicherzustellen, dass Anwendungen und Dienste schneller und zuverlässiger bereitgestellt werden können.

![](https://slabstatic.com/prod/uploads/grxbau6j/posts/images/HZIyS9czUHMAKMQOPczPCtS0.png)

## Unterschied Virtualisierung und Containerisierung

Virtualisierung und Containerisierung sind beide Technologien zur Isolation von Anwendungen und Abhängigkeiten, aber es gibt einige wichtige Unterschiede zwischen ihnen:

Die **Virtualisierung** nutzt eine virtuelle Maschine (VM), um ein vollständiges Betriebssystem und darauf laufende Anwendungen zu isolieren. Jede VM hat eigene Ressourcen.

Die **Containerisierung** nutzt einen Container, um nur die Anwendung und ihre Abhängigkeiten zu isolieren. Containers teilen sich das Betriebssystem des Hosts, wodurch sie weniger Ressourcen verbrauchen und schneller gestartet werden können als VMs. Containers sind für die Portabilität und Übertragbarkeit von Anwendungen ausgelegt und bieten eine höhere Effizienz als VMs.



## Unterschied Image und Container

Ein **Image** ist eine Vorlage für einen Container, die alle notwendigen Dateien und Einstellungen enthält, um eine Anwendung auszuführen. Es kann als «Abbild» einer vollständigen Umgebung für eine Anwendung angesehen werden. Ein Image kann als Vorlage für mehrere Container verwendet werden.

Ein Container ist eine isolierte Instanz einer Anwendung, die auf einem Host ausgeführt wird. Es nutzt das Betriebssystem des Hosts, aber ist durch eine isolierte Umgebung abgeschirmt, sodass es unabhängig von anderen Containern auf demselben Host ausgeführt werden kann. Jeder Container wird aus einem Image erstellt und kann eigene Einstellungen und Daten haben, die unabhängig von anderen Containern sind.



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
