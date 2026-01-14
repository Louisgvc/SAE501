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

![Alt text](https://github.com/Louisgvc/SAE501/blob/main/point%20d'acc%C3%A9s%20guest%20.png?raw=true)

- Nous avons aussi procédé de la même maniere pour un administrateur

Network : Admin

Network => Interfaces => Admin => Edit

General Settings

![Alt text](https://github.com/Louisgvc/SAE501/blob/main/point%20d'acc%C3%A9s%20admin.png?raw=true)

- Device : celui correspondant au réseau wifi (dans mon cas br-lan,
mais cela pourra sans doute être différent)
- IPv4 address : 192.168.3.1
- IPv4 netmask : 255.255.255.0

Firewall Settings
- Create => guest
- Network => Firewall

![Alt text](https://github.com/Louisgvc/SAE501/blob/main/firewall.png?raw=true)

Après création de l’interface réseau « Guest » et admin, configuration du point d’accès Wi-Fi « hotel transylvania » (mode Access Point sans sécurité), association au réseau Guest et définition de l’adresse IP statique 192.168.3.1/24, la configuration est terminée.
La zone firewall « guest » a été créée afin d’isoler complètement les clients du réseau invité du réseau principal (administration).
La capture d’écran présente simultanément :
• le réseau LAN principal (administration)
• le nouveau réseau invité Guest avec son interface radio br-lan et son SSID hotel transylvania

![Alt text](https://github.com/Louisgvc/SAE501/blob/cc51b7c95052fff5839442ebbd9ff516433b6448/nos%20interfaces.png)
