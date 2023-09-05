# [Infra-Dev] Scripting Bash/Powershell sur USB

Project by MARMANDE Mélanie, NAVARRO Mathias

## __Table de matière :__

I. [Mise en bouche](#i---mise-en-bouche)   

- Description de l'idee du projet

- Le materiel requis (trouver une bonne clé à tester, l'os en question, les logiciels, etc...)


II. [Let's get to work](#ii---lets-get-to-work)<br>

__Les problèmes:__

- Problèmes de firmware, problèmes de java et le magnifique cmd windows (: (cry a lot)

- Problèmes materiels aka démonter ta clé usb et faire la manip sans pêter aucun pins (:<

- Coder un script en DuckyScript pour pouvoir automatiquement télécharger et installer une Goose

- Transformer le script en PayLoad avec Duck Encoder

    - [Etape 1](#etape-1-what-to-do-when-we-dont-have-a-ducky)<br>
    - [Etape 2](#etape-2-were-still-not-ducky-lucky-more-issues-lol)
    - [Etape 3](#etape-3-robot-duckynator-searching-for-sarah-connor)

III. [Mon sac est fait !](#iii---mon-sac-est-fait)

__La résolution:__

- PRANK les gens avec sa clé (conclusion du projet)

0 . [Enfin c'est ce qu'on pensait](#0---enfin-cest-ce-quon-pensait)

IV. [Bonus](#iv--bonus-👀)

- Mettre en place un script de vol de mot de passe Windows sur la clé USB

0.5. [For Fun](#05--for-fun)
<br>




# I - Mise en bouche

L'idée est simple: si tu taffes dans un open space et que t'as oublié au moins une fois de verouiller ton pc, tu t'es retrouvé avec un agent de la destruction qui écrit des bêtises sur paint et se bat avec ta souris: la goose (tan tan TAAAAAAAAN!!!!).
Sauf que du coté du pranqueur c'est relou d'a chaque fois devoir aller sur le net, telecharger la goose et la lancer...Et si tu manques de temps pour faire ta bêtise, on préferera trouver une solution plsu rapide et automatiser :)) De là, on va transformer notre clé usb pour quelle soit reconnu comme un appareil HID, soit comme un clavier, qui lancera un script dans une invite de commande qui lui même lancera la goose.

Moral of the story: Windows+L !!!

Jusqu'ici l'idée est belle et parait simple. on va voir au fil de cette aventure a quel point ~~windows est a chier~~ ce n'est pas une mince affaire. C'est pour cela que nous allons essayer de découper au maximum le tout en différent points pour plus de clarté.

First, le matos:

C'est pas tout ca que de cracher sur windows à chaque occasion (meme si c'est absolument necessaire sinon j'explose) mais on va en avoir besoin pour ce projet. La plupart des outils seront sur cette _sublime_ plateforme, dont l'utilitaire pour connaitre la puce de la cle usb qui nous sera necessaire pour plus tard.

# II - Let's get to work !

## __Etape 1:__ What to do when we don't have a ducky
<br>

### __Problème initial: le budget :((__
<br>

Pour faire une clé de prank, il faut pouvoir bidouiller le firmware et la transformer en clavier (HID=(Human Interface Devices) sur google tu verras).

SAUF QUE (sinon c'est pas marrant mdr) toutes les clés ne peuvent pas etre modifiées pour cet usage. Pour des simplifications dans le projet nous aurions pu utiliser une clé dediée à ca, aka une rubber ducky qui est une clé special hacker sur laquelle on peut injecter du code mais le coût est trop élevé pour nous (~80€) nous avons donc testé avec une clé phison 2251-68 (la reference de notre puce).

On a donc utilisé la stratégie "fouiller dans les placards et prier pour avoir une clé compatible".
Le logiciel *flash drive information extractor* nous a permis de tester toutes nos clés et on en a trouvé une! Ici elle aura une puce phison 2251-68, plus de details la dessus plus tard. 

Pour pouvoir faire des bêtises avec il faut ecrire par dessus le firmware de la clé, autrement dit la "flash".
C'est a ce moment la que les choses se complexifient, et que la puce est importante car seulement les puces inferieures a 2303 sont compatibles avec cette manip! *oh no jojo ref*


📷 [FlashDriveInfo](./usb.png)

## __Etape 2:__ We're still not ducky lucky (more issues lol)

Beaucoup d'installation d'applications ou telechargement de code and files/crash test.
Au départ j'ai testé énormément de manières différentes pour que la clé soit reconnue en HID
J'ai notamment tenté de changer ma clé usb classique en clé rubber ducky en passant par l'app usb autorun creator (MPALL Get info).
Malheureusement cela n'a pas fonctionné sur ce format de clé :((
Par la suite j'ai pris le temps de mieux comprendre ce tuto pour faire sa propre bad usb (https://null-byte.wonderhowto.com/how-to/make-your-own-bad-usb-0165419/) et nous avons finalement reussi à bien suivre toutes les étapes.

Télécharger et compiler le code source (va nous permettre de construire les outils qui vont nous permettre d'intérargir avec la clé usb est de la modifier)
Le code source est publié sur GitHub par Adam Caudill (https://github.com/brandonlw/Psychson)

Tout comme elle a dit juste au dessus. Ici les problèmes qu'on a rencontrés se situent au niveau du build des .bat qui permettent de flash le firmware de la clé, grace aux erreurs de cet ✨ _excellent_ ✨ shell qu'est le cmd windows sur lequel on a appris que le *path to* quoi que ce soit n'est pas en fonction du dossier dans lequel on se situe dans le shell. 

Dans ces builds on aura incorporé notre script basé sur le langage de programmation utilisé sur les vraies rubberducky. On cherche a faire lancer le cmd et dedans recuperer le goose.exe préalablement inséré dans la clé pour le lancer! LE MAL SERA FAIT! 


Une fois tout build il nous faut un fichier .bin grace a un outil appelé duckencoder (https://ducktoolkit.com/payload/windows) qui gere le script en rubberducky. Ici nous lui avons demandé de nous faire un script qui va nous download et executer notre goose.exe ainsi que de passer le firewall de windows sinon l'excution ne pourra pas avoir lieu.
Il faut savoir que le prank de desktop goose est de base un zip, il nous a donc fallu trouver un goose.exe sur internet et en recuperer le lien de telechargement pour que le code l'execute.

Cet outil (duckencoder) est un .jar, donc si jamais vous avez touché a Minecraft au moins une fois dans votre vie, vous savez que c'est du java. Java qui ici pose a nouveau des problèmes dans windows et son shell: en fonction de là ou on est il ne detecte pas que java est installé. Il faut donc trouver l'endroit oú java est installé l'incorporer dans les lignes de commandes pour pas faire des _délicieuses_ "unknown error". (╯°□°)╯︵ ┻━┻

## __Etape 3:__ Robot Duckynator searching for Sarah Connor

La clé est actuellement setup, plus qu'a lui dire quoi faire.
Dans le script on peut lui faire faire ce qu'on veut et lui faire écrire/controler l'ordinateur à notre guise (il existe de nombreux scripts assez amusant possibles, notamment sur duckencoder mais ici nous allons nous limiter à ce qui nous est demandé et eviter d'en faire une clé __vraiment__ malveillante).

Le script est en langage Ducky il faudra donc se retrousser les manches, ce n'est pas du bash comme on aura plus l'habitude. Cependant c'est assez puissant pour faire pas mal de betises avec.

[Exemple de script](./exemple%20script%20ducky)


# III - MON SAC EST FAIT!

Une fois le build fait sur la clé, le script écrit et la cible repérée, passage a l'action.
Petit rappel on a ici fait un setup de script qui lance un ".exe" dans un environnement windows, on ne pourra donc qu'infecter un pc sous windows (on vous voit les gens sur linux et mac, vous en faites pas on pense a vous et on planche sur quelque chose pour vous emmerder).

Brancher la clé fera donc instantanément les betises, plus qu'a voir la tete de la victime!

Bon, c'est bien marrant tout ca, on a un petit programme mignon qui fait des petites betises jusqu'au moment ou on appuie longtemps sur echap. Ca reste dans le registre du prank, rien de plus.
Sauf que ici on a un outil TRES PUISSANT. Faisons l'amalgame avec un simple couteau: on peut s'en servir pour couper ses legumes comme pour faire mal a quelqu'un. Tout depend de comment on l'utilise.
En informatique c'est pareil: cet outil peut potentiellement lancer un script qui telecharge un malware qui recupere tout ce que la personne ecrit, les cookies des differents sites dont potentiellement banquaires (donc les identifiants et mots de passes, carte bancaire etc) et qui les envoie sur une boite mail intracabe ou autre.

Avoir acces physique direct au pc c'est la maniere la plus puissante pour le hacking.

# 0 - Enfin, c'est ce qu'on pensait...

Pour être tout à fait correct, la dernière étape est de flasher notre clé pour qu'elle bascule automatiquement le mode de notre USB en mode de démarrage pour flasher le firmware. Et maintenant que notre clé USB est devenue un clavier, nous ne pouvons plus changer de mode à part si nous venons faire une petite manip risqué sur la clé usb en venant connecter deux petit pins de notre microcontrolleur au moment du branchement de la clé. Cette manip si faîtes à la va vite, trop brusquement ou pas correctement, endommagera définitivement notre usb, la rendant impossible à utiliser --> direction poubelle 

Malheureusement après plusieurs tentatives, impossible de flasher la clé

[erreur flash usb](./erreur%20flash.png)

Sortie: erreur 0006

Après pas mal de recherches, j'ai pu tomber sur des personnes ayant le même problème que moi. Le résultat de toutes ces recherches nous ammène au fait que __finalement__ ma clé physon 2251-68 n'est pas compatible pour faire le flash

Voici une liste des clés compatibles pour faire ce projet (https://github.com/brandonlw/Psychson/wiki/Known-Supported-Devices). Au final seulement les clés possédant une puce 2303 sont compatibles pour cet action, __mais__ (sinon c'est pas drôle) elles ne sont plus en production depuis des années déjà et quasiment impossible à trouver sur le marché.

Il nous faudrait donc une clé rubber ducky mais le coût est trop élevé, ou bien hebergé sur un site le goose.exe et le lancé manuellement, mais ce n'est pas dans ce sens là que nous voulions allé pour ce projet :/

Actuellement notre clé fonctionne uniquement sur mon PC car les modifs ont été faites sur ce dernier, donc seulement mon PC le reconnait en tant que HID

[visuel](./exemple%202%20goose.png)


# IV- Bonus 👀

- Mettre en place un script de vol de mot de passe Windows:

Pour faire cette partie j'ai suivie le tuto suivant : (https://www.peterstavrou.com/blog/tech/make-hacking-usb-like-mr-robot/) qui m'a renvoyé sur un lien de téléchargement d'outils de récuperation de mot de passe
 (http://www.nirsoft.net/password_recovery_tools.html)

NirSoft est un site web qui fournit des outils de réparation gratuit de mots de passe pour une variété de programmes Windows, comme Chrome, Firefox, Microsoft Edge, Internet Explorer, Microsoft Outlook, mot de passe de réseau Windows, clés de resau sans fil, entrées d'accès à distance de Windows, et plus...

Mais il a enlevé les options de ligne de commandes qui exportent les mots de passe vers un fichier à partir de tous les principaux outils de récupération de mot de passe car sinon il était censuré.

[my hacking usb](./hacking%20usb.png)

[script de vol de mot de basse (script.bat)](./script%20hacking%20mp)

- Comment rendre cross-platorm: recherches


# 0.5- For Fun

https://github.com/whid-injector/WHID