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
- Un tutorial sur [FreeRadius](raw.githubusercontent.com/Louisgvc/SAE501/main/) 3/4 sera à fournir.

![Alt text](https://raw.githubusercontent.com/Louisgvc/SAE501/main/shem.png "a title")
