# [Infra-Dev] Infrastructure compromise par Rubber Ducky

Project by MARMANDE Mélanie, NAVARRO Mathias

## __Table de matière :__

0.[Intro](#0---intro)

- prolongation du projet du semestre 1 mais avec + de matériel

- revenir sur les points clés projet 1

I. [Debut de l'aventure](#i---début-aventure)

- Description de l'idee du projet

- Le materiel utiliser (achat, stockage, install etc...)

II - [Let's fight](#ii--lets-fight)

[côté hardware](#côté-hardware)

- Problèmes rencontrer lors des install des deux PCs clients et serveurs

- Problèmes lors de la liaison entre les deux (attention à la docu)

[côté script](#côté-script)

- Reussir à s'informer sur les payloads et avoir des pistes sans avoir à payer

- Faire un bon script avec la rubber ducky sans exploser l'ordi

III- [Nos potions magiques](#iii--nos-potions-magiques)

- un peu d'intelligence

(- a voir pour les scripts)

- rapport de projet type cyber une fois infrastructure corrompue

- conclusion et sensibilisation

# 0 - Intro

Ce projet est une prolongation du précédent ou nous avons tenté de transformer une clé usb classique en rubber ducky.
Ce dernier c'était conclu sur un échec cuisant de notre part car qu'une seule puce est actuellement capable de faire ca mais cette dernière n'est plus sur le marché.

Ce projet est donc une suite logique au premier mais avec nettement plus de matériel.

Cette fois, nous avons réussi à nous fournir une rubber ducky grace à la coopération d'YNOV (c'est faux j'ai du la payer, je suis pauvre mtn... anyway).

Nous avons aussi reussi à recupérer chacun un vieux PCs pour les utiliser pour ce projet et ainsi construire une infrastructure.

# I - Début aventure

Le but premier de ce nouveau projet est donc de construire une infrasture physique avec nos deux PCs et ensuite de la compromettre avec notre clé USB.

Pour mettre en place l'infrastructure, nous avons un PC sous Windows Server 2016. Il était au départ en 2019 mais la rubber ducky était détecté donc nous sommes descendus de version.
Ce server à été promue en Domain Controller et nous avons mis en place un Active Directory simple.

Notre machine client, elle est sous windows 10 est sera relié au domaine du DC Windows Server.

Par la suite il fallait aussi préparer notre clé rubber ducky:
Il nous fallait donc écrire un script (utilisation de payload studio pour convertir les scripts en .bin et que cela soit ainsi compatible)

Le but de se dernier est qu'une fois la clé branché sur le client, nous puissions récupérer les informations suivantes de l'infrastructure:
    - IP/FQDN du Domain Controller
    - Informations réseau
    - Mots de passe de la machine
    - Mots de passe des serveurs

Et pour finir installez une backdoor de notre choix sur le client, il y a énormément de manière différente de pouvoir s'y prendre(reverse shell, cheval de troie, mail piégé, phishing etc. . .)

# II- Let's fight

Bien entendue, lors de ce projet nous avons aussi rencontré notre lot de difficultés, malgré que cela soit plutôt un manque de temps et de documentation qui fait que ce projet ne sera pas finit à temps.

## Côté Hardware

Côté Hardware il à déjà fallu trouver DEUX PCs en dehors du notre actuel, qui soit assez ancien mais qu'il ait suffisamment de ram pour faire tourner un serveur, et que nous n'ayons pas peur de les faire pêter car c'est une infrastructure PHYSIQUE.
Cette première étape nous à déjà pris un peu de temps, un PC que j'avais amené n'arrivait pas à boot sur le windows server et un autre PC avait le clavier totalement pété ce qui nous as posé quelques problèmes.

Nous avons finalement réussi à trouver deux PCs à peu près correct pour les relier et faire l'infrasture. Les install ont commencé.
Windows 10 sur le client as du etre reinstallé plusieurs fois car problèmes avec l'ordi.

Et pour le serveur nous avions au départ installé la version 2019. Seulement pour ce projet il fallait que la rubber ducky ne soit pas détécté par le client, si c'était le cas il fallait mettre la version 2016, ce qu'on a du faire. . .

Nous avons donc dès le départ perdue énormément de temps en install.

Quelques "problèmes" rencontrés sur le serveur quand nous avons voulue en Domain Controller. Nous n'avions pas internet...
Nous étions à l'école donc pas de cable, ni de prise ethernet.Et nous avions beau activé le Wifi [he was turned on but turned off](./turned%20on%20but%20off)

Au bout de BEAUCOUPPPPPP de temps, nous avons pu voir (grace à notre dirlab) qu'il y avait simplement un bouton SUR l'ordi pour activer ou non la Wifi (*stupid)
Brefff, tout ca pour dire aller à l'école les enfants ou chez l'ophtalmo à ce niveau (attention aux vieux ordi il avait pas mal de technologies)

Bon, magré tout on va nous accorder un point, le serveur n'avait pas de Wifi préinstallé, ce qui est assez rare tout de même, nous avons du l'ajouter à la main.

De plus attention à la documentation sur les serveurs, surtout celles de Microsoft, elles sont pourries.

## Côté Script

Côté script, il a fallu attendre que la rubber ducky arrive car elle vient des US et elle à été un long moment bloqué à la douane, il a donc fallu attendre au moins 2 séances avant de la recevoir, ce qui à aussi énormément ralentit les avancées du projet. 

Par la suite, il a fallu APPRENDRE à s'en servir, ce qui n'a pas été évident pour moi au début. Il m'a fallu une séance pour comprendre que (logiquement) elle prenait mes scripts comme si ils étaient en clavier US alors que le mien est FR. J'ai donc ensuite trouvé un site (studio payloads) qui m'a permis de convertir mes scripts en fichier .bin en choississant la langue( que ce soit US,Fr, GB etc...)

Actuellement j'ai des soucis avec le script, ils ne sont pas fonctionnels et je ne comprends pas pourquoi. Et le peu de ressources (qui était incroyables) qu'il existait sur les scripts de rubber ducky ont été bann de google ou github (car ca reste des informations qui mal utilisés peuvent faire du mal, cela reste dans un cadre assez illégale).

# III- Nos potions magiques

Une fois l'infrasture compromisse et donc toutes les données des machines récuperer par la rubber ducky, nous pourrions écrire un rapport d'intervention sur les problèmes qui ont eu lieu, comment c'est arrivé et comment "réparer" l'infrastructure.

Nos solutions:
- bcp de recherches, de temps de réflexion

Nous n'avons pas été confronté à des problèmes non resoulables comme au premier projet par des problèmes de matériel, c'est à ce niveau manque de temps, de connaissances et de documentations.

A savoir que nous avons fait tout ca pour des raisons de recherches et académiques et non dans un bute malveillant.
### Bonus

- Installez une machine CentOS 8 ou Debian
    - Installer un annuaire LDAP tout simple sur le serveur
    - Installer un serveur web
- Créez une autre machine Ubuntu
- Répétez les mêmes opérations en reliant la machine Ubuntu au domaine
- Ecrire un rapport sur votre intervention
    - Précisez l’infrastructure mise en place
    - Indiquez les objectifs
    - Indiquez les opérations effectuées
    - Expliquez les failles exploitées, côté matériel et logiciel
    - Trouvez des moyens de remédier à ces failles

Organisation: https://trello.com/b/8GpjtWRY/rubberducky2