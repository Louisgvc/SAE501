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


![Alt text](https://github.com/Louisgvc/SAE501/blob/7dbb383e005f431b6dd5bcec8855b8f2e8a6062d/2025-12-19_11-25.png)

![Alt text](https://github.com/Louisgvc/SAE501/blob/8ba5f10dd92904cbfbf2bf284480b7ca02a272e5/Connexion%20apr%C3%A9s%20redirection%20vers%20notre%20portail%20captif.png)


![Alt text](https://github.com/Louisgvc/SAE501/blob/8ba5f10dd92904cbfbf2bf284480b7ca02a272e5/redirection%20vers%20notre%20portail%20captif.png)

![Alt text](https://github.com/Louisgvc/SAE501/blob/cc51b7c95052fff5839442ebbd9ff516433b6448/erreur%20apres%20un%20faux%20mot%20de%20passe%20.png)
