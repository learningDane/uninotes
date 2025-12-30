#seminar 
11/12/2025: Tecnologia ROS applicata allo sviluppo di un veicolo a guida autonoma

Ingegner Neri Marco
Ingegner Angelo Mineo

SMARTENGINEERING S.p.A. è una azienda di consulenza in ingegneria industriale.
# Veicolo a guida autonoma
Un veicolo a guida autonoma è un veicolo in grado di rilevare l'ambiente tramite una serie di sensori e muoversi da un punto A ad un punto B senza l'intervento umano.

Un veicolo a guida autonoma, dotato di sensori, attuatori e mappe, implementa i moduli di percezione e di localizzazione, passa poi alla pianificazione ed infine al controllo.

# ROS: Robotic Operating System
ROS è un meta-sistema operativo open source per sistemi robotici.
Fornisce i servizi che ci si aspetta da un sistema operativo:
- astrazione dell'hardware
- controllo dei dispositivi a basso livello
- implementazione di funzionalità comuni
- passaggio di messaggi tra processi

Perché "meta"-sistema operativo?
ROS è un framework middleware progettato per lo sviluppo di software per la robotica, quanto segue è lo stack inplementativo di ROS:
1. hardware
2. [[Linux]] OS
3. ROS middleware
4. ROS library
5. Application
## Storia
ROS è stato pensato e creato da Keenan Wyrobek ed Eric Berger nel 2006, la prima versione ufficiale, "Box Turtle" esce nel 2010.
Nel 2013 la gestione viene trasferita alla **Open Source Robotics Foundation** (OSRF).
Nel 2016 esce ROS2, migliorando la modularità, la portabilità e la sicurezza del sistema.
## Dettagli
ROS utilizza una architettura modulare.
ROS fornisce strumenti per l'allocazione equa delle risorse, evitando che un nodo o un processo monopolizzi l'elaborazione della [[CPU]].
ROS è organizzato in nodi.
## Componenti di ROS
- Rviz: strumento di visualizzazione 3D che permette di visualizzare i dati sensoriali, modelli robotici e altre informazioni
- Gazebo: simulatore robotico 3D avanzato che consente di creare un mondo virtuale per le simulazioni
- **nodo**: un nodo è un processo autonomo che esegue un compito specifico
- il nodo "slam" (simultaneous localization and mapping), insieme al nodo "teleoperation" (responsabile del controllo del robot), consente di costruire la mappa dell'ambiente in cui si trova il veicolo
- li nodo "navigation" è responsabile di generare un percorso per il robot sulla base di:
	- mappa
	- posizione iniziale
	- informazioni dai sensori
- **topic**: sono i canali di comunicazione dove i nodi pubblicano e sottoscrivono messaggi. Il modello publish-subscribe è un paradigma di comunicazione asincrona tra i nodi del sistema.
- **servizio**: è un meccanismo di comunicazione sincrono tra i nodi, permette ad un nodo di richiedere una azione specifica e ricevere una risposta.
## Utilities di ROS
Un file `.launch` è un XML che specifica come avviare un insieme di nodi e configurazioni del sistema.
```shell
roslaunch nomeFile.launch
```
# Esempio
```shell
# lancia gazebo
roslaunch turtlebot3_gazebo turtlebot3
```