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

![Alt text](https://github.com/Louisgvc/SAE501/blob/65829e0f6ddafbcc67d1050558df541c0c79961f/Image/wrt1200ac/point%20d'acc%C3%A9s%20guest%20.png)

- Nous avons aussi procédé de la même maniere pour un administrateur

Network : Admin

Network => Interfaces => Admin => Edit

General Settings

![Alt text](https://github.com/Louisgvc/SAE501/blob/65829e0f6ddafbcc67d1050558df541c0c79961f/Image/wrt1200ac/point%20d'acc%C3%A9s%20admin.png)

- Device : celui correspondant au réseau wifi (dans mon cas br-lan,
mais cela pourra sans doute être différent)
- IPv4 address : 192.168.3.1
- IPv4 netmask : 255.255.255.0

Firewall Settings
- Create => guest
- Network => Firewall

![Alt text](https://github.com/Louisgvc/SAE501/blob/65829e0f6ddafbcc67d1050558df541c0c79961f/Image/wrt1200ac/%20firewall.png)

Après création de l’interface réseau « Guest », configuration du point d’accès Wi-Fi « hotel transylvania » (mode Access Point sans sécurité), association de ce SSID à l’interface Guest et définition d’une adresse IP statique 192.168.3.1/24, la configuration du réseau invité est terminée.

La zone firewall « guest » a été créée spécifiquement pour isoler complètement les clients du réseau invité du réseau principal (administration). Cette zone est configurée sans forwarding vers la zone « lan » et sans accès aux services internes (DHCP, DNS, etc. du réseau admin).

La zone firewall par défaut « lan » reste quant à elle associée au réseau d’administration (interface LAN principale, généralement 192.168.1.1/24 ). Elle autorise le forwarding vers la zone « wan » (accès Internet) et protège les services internes du routeur (LuCI, SSH, etc.) tout en restant inaccessible depuis la zone « guest ».

La capture d’écran globale présentée ci-dessous montre simultanément :

• le réseau LAN principal (administration) avec sa zone firewall « lan »

• le nouveau réseau invité Guest avec son interface radio br-lan, son SSID HotspotRT

• les zones firewall correspondantes (« lan » et « guest ») illustrant la séparation claire entre les deux réseaux

![Alt text](https://github.com/Louisgvc/SAE501/blob/65829e0f6ddafbcc67d1050558df541c0c79961f/Image/wrt1200ac/nos%20interfaces.png)

Réseau invité fonctionnel :

SSID hotel transylvania (ouvert) → interface Guest (192.168.3.1/24)

Firewall zone « guest » créée → isolation OK

Les deux réseaux (admin + guest) cohabitent correctement comme le montre cette vue globale.

Et ci-dessous nous avons nôtre redirection et connexion de nôtre portail captif : 

![Alt text]([https://github.com/Louisgvc/SAE501/blob/main/redirection%20vers%20notre%20portail%20captif.png?raw=true](https://github.com/Louisgvc/SAE501/blob/65829e0f6ddafbcc67d1050558df541c0c79961f/Image/opensense/redirection%20vers%20notre%20portail%20captif.png))


