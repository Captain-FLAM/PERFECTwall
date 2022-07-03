# PERFECT wall

Le premier Firewall 100% open-source pour Windows 8/10/11 basé sur les noms de domaine !

J'ai besoin d'aide pour avancer plus vite : Ce projet est ouvert à toute les bonnes volontés.

Vous pouvez me contacter par [e-mail](https://github.com/Captain-FLAM)  
Et j'ai aussi activé le module [Discussions de GitHub](https://github.com/Captain-FLAM/PERFECTwall/discussions)

### CARACTÉRISTIQUES
#### de la version 0.5 (Je travaille encore dessus)

* Multilingue (Français & Anglais, pour l'instant)  
Vous pourrez ajouter des langues très facilement grâce à de simples fichiers INI encodés en UTF-8.
* Affiche les requêtes DNS avant qu'elle ne soit envoyées  
Pour l'instant, il s'agit d'une simple liste (type journal)
* Indique les connexions réseau en temps réel sur l'icone de la barre des tâches

### INSTALLATION

Suivez le guide dans le [WIKI](wiki/Installation%20(FR).md)

### BIOGRAPHIE

Programmeur depuis l'âge de 12 ans (1981).  
Avant, je développais en ASM, C, C++, Basic, Visual Basic.  
Depuis l’an 2000, je code en PHP, MySQL, JavaScript, jQuery, HTML, CSS.  
Et aujourd'hui, en C# pour ce projet.

### HISTORIQUE

Sous Windows 98 et XP, j’utilisais « Kerio Firewall » et sous Windows 7, « PC Tools Firewall ».  
Ces deux-là me convenaient bien, car ils affichaient l’URL demandée par chaque logiciel.

Mais depuis Windows 10, catastrophe !

Tous les pare-feux actuels fonctionnant sous Windows 10 sont orientés IP (Comodo, ZoneAlarm, Outpost, et celui intégré à Windows et ceux qui l'utilisent : WFC de Binisoft, TinyWall, WFN de WoKhan, ...)

A part « Free Firewall » (de Evorim), mais qui ne fonctionne pas bien, ne contrôle que les connexions sortantes et n’est pas open-source.

Et à part « PortMaster », que je viens de découvrir récemment et qui correspond à l’idée que je me fais, mais qui est écrit en GO et qui télécharge 300 Mo de dépendances !  
Certains seront pleinement satisfaits par cette solution , que vous pouvez voir ici : [github.com/safing/portmaster](https://github.com/safing/portmaster)

Mais c’est très loin de l’idée que je me fais d’un Firewall léger, rapide et qui occupe peu de place en mémoire !!

### CONSTAT

1. Depuis le premier Windows que j'ai utilisé (version 3.1) jusqu'à aujourd'hui, je n'ai jamais connu un Firewall **100% Open-Source** basé sur les noms de domaine !
2. Je pense que c’est un non-sens de bloquer des IP, car un serveur peut héberger plusieurs sites web sous la même IP !
3. De plus, comment savoir si l’on souhaite autoriser une règle de pare-feu sans savoir à quoi correspond l’IP affichée (sans se faire chier à faire une recherche web) ?

Solution : Bloquer plutôt des noms de domaines, ou des groupes d’IP de serveurs appartenant à des entreprises.

### UN VIEUX RÊVE

Depuis 2014, je rêve d’un pare-feu idéal et j’ai collecté tout un tas d’informations et de codes sources, mais je n’ai rien trouvé de convaincant.  
Ces derniers temps, j’ai consulté les archives de mes fichiers capturés et cela m’a donné envie de voir ce qu’il y avait de nouveau sur le web...  
Lors de recherches hasardeuses, je suis tombé sur un pilote qui peut correspondre à mes critères de filtrage et de là, me voilà reparti sur ce projet de dingue !  

### LE PARE-FEU IDÉAL ?

Je rêve d’un Pare-feu qui me conseille intelligemment sur ce que je dois décider et qui ne me harcèle pas trop, tout en assurant ma tranquillité d’esprit ...

Ce serait un pare-feu applicatif (règles différentes par application, ce qui est déjà le cas de la plupart) mais avec un filtrage par noms de domaine, ou par groupes d’IP, ou par IP le cas échéant.  
Par exemple :  
Autoriser la connexion de « Windows Update » aux IP appartenant UNIQUEMENT à Microsoft.  
Refuser la connexion de « Firefox » au service de ping de Mozilla.  
Refuser la connexion de « Windows » au service « Compte » de Microsoft. ( → login.live.com)

Avec des règles globales simples, par exemple :  
Autoriser / Refuser globalement les services nécessaires pour « Windows Update » (BITS, WuauServ, Orchestrator, etc.)  
Fini les Hacks dans la base de registre pour empêcher les mises à jour intempestives !  
Ainsi, mon Windows ne se mettrait à jour QUE lorsque je l’aurai décidé !

et bien sûr :  
Refuser complètement à un programme de se connecter à internet !  
(c’est-à-dire : pas de requêtes DNS non plus : gain de temps, moins de threads en attente, économie de batterie sur les portables, plus de bande réseau disponible, moins de pollution électrique, etc.)

Croyez-moi, si vous saviez le nombre de connexions inutiles par minute, par heure, par jour qui partent de votre PC, vous seriez effarés !  
D’ailleurs grâce à **PERFECT wall** , vous allez vous en rendre compte.

Multipliez ça par des milliards de PC ...  
Pour réduire le réchauffement climatique, commençons par réduire les accès de nos PC !!

### SOLUTIONS UTILISÉES

**PERFECT wall**  
**&copy; Captain FLAM - 2022**  
Codé en C# avec WFP/XAML pour du prototypage rapide, mais le pilote (WinDivert) est codé en C.  
Par la suite, certaines parties pourront être recodées en C ou C++ pour être plus performantes.

J’ai choisi d’utiliser la version de .NET 4.5 au minimum pour que les gens n’aient pas besoin d’installer d’autres dépendances que Visual C++ (14 Mo au minimum, voire pas du tout s’il y a déjà une version supérieure installée).

**WinDivert** - (codé en C)  
**&copy; Basil00**  
Ce pilote est génial !  
J'ai juste modifié la DLL pour rendre l'installation du pilote permanente dans "C:\Windows\System32".
J'ai également créé un processus d'installation (install.cmd & setup.exe) pour faciliter les choses.

> Windows Packet Divert (WinDivert) is a user-mode packet interception library
> for Windows 7, Windows 8 and Windows 10.
> 
> In summary, WinDivert can:  
> - capture network packets  
> - filter/drop network packets  
> - sniff network packets  
> - (re)inject network packets  
> - modify network packets

**WinDivertSharp** - (codé en C#)  
**&copy; Jesse Nicholson « TechnikEmpire » - (Ontario, Canada)**  
Cette interface a été créée pour la version 1.4 de Windivert et j’ai repris profondément tout le code pour qu'il fonctionne avec la version 2.2 de WinDivert, et de plus je l'ai simplifié.

**Hardcodet NotifyIcon for WPF** - (codé en C# / WPF / XAML)  
**&copy; Philipp Sumi - (Switzerland)**  
J'ai du adpater le code de la dernière version (1.1.0) pour qu'il fonctionne avec le Framework .NET 4.5.

> Il s'agit d'une implémentation d'un NotifyIcon (alias icône de la barre des tâches) pour la plate-forme WPF.
> Il ne repose pas seulement sur le composant "Windows Forms NotifyIcon", mais c'est un contrôle purement
> indépendant qui exploite plusieurs fonctionnalités du framework WPF afin d'afficher des info-bulles riches,
> des fenêtres contextuelles, des menus contextuels et des messages de bulle.

**INI File Parser** - (codé en C#)  
**&copy; Ricardo Amores Hernández - (Barcelona)**  
Cette librairie par ne s'appuie pas sur les API de Win32, et par conséquent supporte l'UTF-8.  

J’ai inclus juste le nécessaire dans ce projet, mais si vous souhaitez voir le reste (exemples, tests et autres) :  
[github.com/basil00/Divert](https://github.com/basil00/Divert)  
[github.com/TechnikEmpire/WinDivertSharp](https://github.com/TechnikEmpire/WinDivertSharp)  
[github.com/hardcodet/wpf-notifyicon](https://github.com/hardcodet/wpf-notifyicon)  
[github.com/rickyah/ini-parser](https://github.com/rickyah/ini-parser)

### ROADMAP

- Bloquer les noms de domaines par application
- Vérifier ou ne pas vérifier les noms de domaines par application  
(ex : Ne pas vérifier pour BitTorrent.exe, car les connexions se font par IP)
- Rediriger les requêtes par nom de domaine et par protocole  
(ex : www.XXX.com port 80 → 127.0.0.1 port 64080 : page HTML renvoyée « Connexion bloquée »)
- Autoriser/Bloquer les requêtes par groupes d’entreprises (évite la télémétrie, le DNS poisoning, etc.)
- Autoriser / Refuser simplement les services nécessaires par groupes, au jour le jour  
(ex : Réseau Local (LAN), Windows Update, Visual Studio, etc.)
- Conseiller intelligemment sur les actions à prendre pour les services abscons de Windows avec un panneau d’information complet  
(ex : Connexion Netbios → « Utilisez-vous un réseau local ? » OUI/NON : Interdire tous les services de réseau local d’un seul coup)
- Et dans le futur et pour les plus paranos d'entre-vous qui ne font pas confiance au WFP de Microsoft, j'aimerais pouvoir développer un pilote NDIS 6.0 dans le même esprit que « WinpkFilter » (qui n'est pas open-source)

Bonus : J’aime bien voir l’activité de mon réseau en un coup d’œil et à part Comodo aucun ne dispose d’un indicateur visuel, excepté bien sûr **PERFECT wall** !

### COMPILATION

Suivez le guide dans le [WIKI](wiki/Compilation%20(FR).md)

### REMERCIEMENTS

**Icônes trouvées sur "Pixabay.com"**  
Bouclier par <a href="https://pixabay.com/fr/users/openclipart-vectors-30363/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=154885">OpenClipart-Vectors</a>  
Paramètres par <a href="https://pixabay.com/fr/users/openicons-28911/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=98391">OpenIcons</a>

P.S :  
Avant que quelqu’un ne me le demande : Je sais bien que certains pare-feux offrent des fonctionnalités supplémentaires (Vérification des signatures numériques, anti-intrusion, etc.) mais ce n’est pas prévu pour l’instant dans ce projet.

**&copy; Captain FLAM - 2022**  
@ Licence MIT
