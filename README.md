## Sujet 4 – Mise en place d’un hotspot Wifi et gestion des clients

La première partie de ce projet est identique au sujet précédent:
- Mise en place d’un hotspot WiFi, tel qu’on pourrait trouver dans un hôtel
ou un centre de vacances. Il faut donc prévoir le portail captif, la
séparation du réseau client et du réseau administration,
l’enregistrement des logs des clients.
- Dans la deuxième partie, au lieu d’attaquer votre réseau WiFi (ce qui
n’empêche pas de bien le sécuriser), on ajoutera une base de données
de clients à qui on autorisera l’accès au WiFi. Pour cela, on devra
mettre en place un radius, de type Freeradius 3 (voir 4). Dans un
premier temps, la base de données sera intégrée au FreeRadius. Une
fois fonctionnel, on créera une base de données externes.
- Dans les logs, on devra retrouver l’identité des clients qui se seront
connectés sur une journée.
- Un tutorial sur [FreeRadius](daloradius.md) 3/4 sera à fournir.
 

![Alt text](https://raw.githubusercontent.com/Louisgvc/SAE501/main/shem.png "a title")

Dans la mise en place d'un hotspot wifi, nous allons effectuer des configurations plus avancées d’un point d’accès que ce
qui a été fait l’an dernier. Ainsi, nous allons pouvoir utiliser des paquets installables sur le
firmware OpenWRT, par exemple intégrer un portail captif. 

1- Mise en place de l’accès entreprise hotel transylvania avec OpenWRT

L’accès entreprise sera mise en place avec le routeur Linksys WRT1200ac. 

- Sur le point d’accès, dans :
System => Administration => Activer le SSH sur l’interface LAN.

- Nous allons préparer le point d’accès pour la suite.

Voici un lien qui explique relativement bien la marche qu'on a suivi :
https://oldwiki.archive.openwrt.org/doc/recipes/guest-wlan-webinterface

Voici les différents menus que nous avons configurer :
- Network => Interfaces =>

Name : Guest
Protocol : Static address

Device : A préciser une fois que le réseau wifi sera créé

- Network => Wireless =>
Nous avons crée un accès avec le SSID « hotel transylvania »

mode AP 

sans sécurité

Network : Guest

Network => Interfaces => Guest => Edit

General Settings

- Device : celui correspondant au réseau wifi (dans mon cas br-lan,
mais cela pourra sans doute être différent)
- IPv4 address : 192.168.3.1
- IPv4 netmask : 255.255.255.0

Firewall Settings
- Create => guest
- Network => Firewall

![Alt text](https://github.com/Louisgvc/SAE501/blob/cc51b7c95052fff5839442ebbd9ff516433b6448/nos%20interfaces.png)

2- Réalisation d’un portail captif sur le point d’accès avec
OpenNDS

![Alt text](https://github.com/Louisgvc/SAE501/blob/7dbb383e005f431b6dd5bcec8855b8f2e8a6062d/2025-12-19_11-25.png)

![Alt text](https://github.com/Louisgvc/SAE501/blob/8ba5f10dd92904cbfbf2bf284480b7ca02a272e5/Connexion%20apr%C3%A9s%20redirection%20vers%20notre%20portail%20captif.png)


![Alt text](https://github.com/Louisgvc/SAE501/blob/8ba5f10dd92904cbfbf2bf284480b7ca02a272e5/redirection%20vers%20notre%20portail%20captif.png)

![Alt text](https://github.com/Louisgvc/SAE501/blob/cc51b7c95052fff5839442ebbd9ff516433b6448/erreur%20apres%20un%20faux%20mot%20de%20passe%20.png)
