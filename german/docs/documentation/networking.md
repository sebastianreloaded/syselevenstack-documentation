# SysEleven Stack Networking Service

[TOC]

## Übersicht

SysEleven Stacks Networking Service basiert auf dem OpenStack Neutron Projekt.

Damit kannst du Network-Connectivity-as-a-Service für andere Dienste im SysEleven Stack nutzen, wie zum Beispiel den Compute Service.
Außerdem stellt es Usern eine API zur Verfügung um Netzwerke zu definieren und um bestehende anzupassen.

Du hast zwei Möglichkeiten dein Netzwerk zu verwalten. Du kannst dafür die öffentliche OpenStack API benutzen, genau so wie das [Dashboard](https://dashboard.cloud.syseleven.net).

### Wie verbinde ich 2 Subnetze miteinander?

####Vorraussetzungen:
* Zugang zum [Dashboard](https://dashboard.cloud.syseleven.net)
* mindestens 2 vorhandene Router/Netzwerke
* verschiedene IP-Ranges in beiden Netzwerken

####Schritt Eins: Login

Mit den von SysEleven erhaltenen Daten für Nutzername und Passwort loggen wir uns im [Dashboard](https://dashboard.cloud.syseleven.net) ein.

![SysEleven Login](../img/login_router.png)

####Schritt Zwei: Interface im Router anlegen

Um ein Interface einzurichten, gehne wir wie folgt vor:
* Klicke in der linken Seitenleiste unter "Network" auf "Router
* Nun wählen wir den ersten Router für unsere Verbindung aus und klicken auf den Namen
* Im sich nun öffnenden Fenster gehen wir auf den Reiter "Interfaces" und wählen dort "Add Interfaces" aus.
* Hier wählt man im ersten Punkt den Ziel Router aus, vergibt unter IP eine eigene IP-Adresse (aus der IP-Range des Ziel Routers) und geht dann auf "Submit"

Diese Schritte wiederholt man nun für den anderen Router.

![Interface Übersicht](../img/router-interface.png)

####Schritt Drei: Static Route erstellen

Der nächste Schritt ist nun eine Static Route (Statische Verbindung) anzulegen.
* Wir begeben uns wie vorigen Schritt über "Network" -> "Routers" auf den entsprechenden Router
* Hier klicken wir statt auf "Interfaces" auf "Static Route"
* Nun legen wir eine Static Route über "Add Static Route" an und geben dort die IP-Range des Zielnetzes an, sowie als Nexthop die gleiche IP-Adresse wie im [vorigen Schritt](https://github.com/syseleven/syselevenstack-documentation/blob/master/german/docs/documentation/networking.md#schritt-zwei-interface-im-router-anlegen)

Auch das wiederholen wir für den anderen Router.

![Interface Übersicht](../img/static-route.png)

####Schritt Vier: Hostroute anlegen

Als letzten Schritt benötigen wir noch eine Hostroute.
* Dafür gehen wir in der Seitenleiste nun auf Network, wählen unser Netzwerk aus und klicken auf den Namen.
* Dort sehen wir alle zugehörigen Subnetze, klicken bei dem zugehörigen Subnet auf "Edit Subnet" und wählen den Reite "Subnet Details".
* Unter dem Punkt "Host Routes" können wir unsere Route festlegt.
* Dafür legen wir unseren Ziel IP-Bereich fest (z.B. 10.0.0.0/24) und auch die IP Adresse des dazugehörigen Router Interfaces.
* Mit "Submit" speichern wir nun auch diesen Schritt

Auch diesen Schritt wiederholen wir für das andere Subnet.

![Interface Übersicht](../img/hostroute.png)

####Fazit

Nun haben wir zwei Subnetze verbunden, die untereinander kommunizieren können.<br>
Außerdem haben wir eine eigene Hostroute angelegt und auch verschiedene Unterpunkte im Dashboard kennengelernt.
