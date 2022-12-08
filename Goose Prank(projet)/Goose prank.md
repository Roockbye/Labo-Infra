# [Infra-Dev] Scripting Bash/Powershell sur USB

Project by MARMANDE Mélanie, NAVARRO Mathias

## __Table de matière :__
I. [Mise en bouche](#i---mise-en-bouche)   

Mise en bouche (pour des petits noobs tels que nous):

-- chercher a nuire et comment (description de l'idee du projet)

-- le materiel requis (trouver une bonne cle la tester, l'os en question, les logiciels etc)


II. [Let's get to work](#ii---lets-get-to-work)<br>

Les problemes:

-- problemes de firmware, problemes de java et le magnifique cmd windows (: cry a lot

-- problemes materiels aka demonter ta propre cle usb (:<

-- Coder un script en DuckyScript pour pouvoir automatiquement télécharger et installer une Goose

-- Transformer le script en PayLoad avec Duck Encoder

- [Etape 1](#etape-1-what-to-do-when-we-dont-have-a-ducky)<br>
- [Etape 2](#etape-2-were-still-not-ducky-lucky-more-issues-lol)
- [Etape 3](#etape-3-robot-duckynator-searching-for-sarah-connor)

III. [Mon sac est fait !](#iii---mon-sac-est-fait)

La resolution:

-- PRANK les gens avec sa clé (conclusion du projet)

-- PRANK leur banque en recuperant les logs (ou comment ce serait possible) (lien video yt qui explik mieu) conclusion plus globale

IV. [Bonus](#iv--bonus-👀)

-- Rendre le projet cross-platform (Windows, Mac et Linux)

-- Mettre en place un script de vol de mot de passe Windows sur la clé USB

<br>




# I - Mise en bouche

L'idée est simple: si tu taffes dans un open space et que t'as oublié au moins une fois de verouiller ton pc, tu t'es retrouvé avec un agent de la destruction qui ecrit des betises sur paint et se bat avec ta souris: la goose (tan tan TAAAAAAAAN!!!!). 
Sauf que du coté du pranqueur c'est relou d'a chaque fois devoir aller sur le net, telecharger la goose et la lancer... On va automatiser ca. De la, une cle usb qui sera transformé en clavier automatiser, qui lancera un script dans une invite de commande qui lui meme lancera la goose.

moral of the story: windows L !!! 

Jusqu'ici l'idée est belle et parait simple. on va voir au fil de cette aventure a quel point ~~windows est a chier~~ ce n'est pas une mince affaire. 

le matos:

c'est pas tout ca que de chier sur windows a chaque occasion (meme si c'est absolument necessaire sinon j'explose) mais on va en avoir besoin pour ce projet. La pluspart des outils seront sur cette _sublime_ plateforme, dont l'utilitaire pour connaitre la puce de la cle usb qui nous sera necessaire pour plus tard.

Pour des simplifications dans le projet nous aurions pu utiliser une clé rubber ducky mais le coût est trop élevé nous avons donc testé avec une clé phison 2251-68 (la reference de la puce).
 



# II - Let's get to work !

## __Etape 1:__ What to do when we don't have a ducky

probleme initial: le budget :((

Pour faire une cle de prank, il faut pouvoir bidouiller le firmware et la transformer en clavier (HID sur google tu verras).
SAUF QUE (sinon c'est pas marrant mdr.) toutes les cles ne peuvent pas etre modifiées pour cet usage. Le plus simple serait une cle dediée a ca, aka une rubber ducky qui est une clé special hacker sur laquelle on peut injecter du code. Le souci c'est que ca coute 60 balles. Voila.
On a donc utilisé la strat "fouiller dans les placards et prier pour avoir une cle compatible".
le logiciel *flash drive information extractor* nous a permis de tester toutes les cles et on en a trouvé une! ici elle aura une puce phison 2251-68, plus de details la dessus plus tard. 

Pour pouvoir faire des betises avec il faut ecrire par dessus le firmware de la cle, autrement dit la "flash".
C'est a ce moment la que les choses se complexifient, et que la puce est importante car seulement les puces inferieures a 2303 sont compatibles avec cette manip! *oh no jojo ref*

Déterminer le microcontrolleur de notre usb flash drive avec l'application flash drive information extractor

Pour des simplifications dans le projet nous aurions pu utiliser une clé rubber ducky mais le coût est trop élevé nous avons donc testé avec une clé phison 2251-68

📷 [FlashDriveInfo](./usb.png)

## __Etape 2:__ We're still not ducky lucky (more issues lol)

Beaucoup d'installation d'applications ou telechargement de code and files/crash test.
telecharger et compiler le code source(va nous permettre de construire les outils qui vont nous permettre d'intérargir avec la clé usb est de la modifier)
Le code source est publié sur GitHub par Adam Caudill (https://github.com/brandonlw/Psychson)

Tout comme elle a dit juste au dessus. Ici les problemes qu'on a rencontrés se situent au niveau du build des .bat qui permettent de flash le firmware de la clé, grace aux erreurs de cet  ✨ _excellent_ ✨ shell qu'est le cmd windows sur lequel on a appris que le *path to* quoi que ce soit n'est pas en fonction du dossier dans lequel on se situe dans le shell. 

Dans ces builds on aura incorporé notre script basé sur le langage de programmation utilisé sur les vraies rubberducky. Dans ce script on cherche a faire lancer le cmd et dans ce cmd recuperer le goose.exe préalablement inséré dans la clé pour le lancer! LE MAL SERA FAIT! 

Une fois tout build il nous faut un fichier .bin grace a un outil appelé duckencoder qui gere le script en rubberducky. Cet outil est un .jar, donc si jamais vous avez touché a Minecraft au moins une fois dans votre vie, vous savez que c'est du java. Java qui ici pose a nouveau des problemes dans windows et son shell: en fonction de la ou on est il ne detecte pas que java est installé. Il faut donc trouver l'endroit oú java est installé l'incorporer dans les lignes de commandes pour pas faire des _délicieuses_ "unknown error". (╯°□°)╯︵ ┻━┻

## __Etape 3:__ Robot Duckynator searching for Sarah Connor

La clé est actuellement setup, plus qu'a lui dire quoi faire.
Dans le script on peut lui faire faire ce qu'on veut et lui faire ecrire/controler l'ordinateur a notre guise.

Le script est en langage Ducky il faudra donc se retrousser les manches, ce n'est pas du bash comme on aura plus l'habitude. Cependant c'est assez puissant pour faire pas mal de betises avec.


<!-- J'ai testé différentes manières pour que la clé soit reconnue en HID
J'ai notamment tenté de changer ma clé usb classique en clé rubber ducky en passant par l'app usb autorun creator (MPALL Get info).
Malheureusement cela n'a pas fonctionné sur ce format de clé :((

-->

# III - MON SAC EST FAIT!

Une fois le build fait sur la clé, le script ecrit et la cible repérée, passage a l'action.
Petit rappel on a ici fait un setup de script qui lance un ".exe" dans un environnement windows, on ne pourra donc qu'infecter un pc sous windows (on vous voit les gens sur linux et mac, vous en faites pas on pense a vous et on planche sur qqch pour vous emmerder).

Brancher la clé fera donc instantanément les betises, plus qu'a voir la tete de la victime!

Bon, c'est bien marrant tout ca, on a un petit programme mignon qui fait des petites betises jusqu'au moment ou on appuie longtemps sur echap. Ca reste dans le registre du prank, rien de plus.
Sauf que ici on a un outil TRES PUISSANT. Faisons l'amalgame avec un simple couteau: on peut s'en servir pour couper ses legumes comme pour faire mal a quelqu'un. Tout depend de comment on l'utilise.
En informatique c'est pareil: cet outil peut potentiellement lancer un script qui telecharge un malware qui recupere tout ce que la personne ecrit, les cookies des differents sites dont potentiellement banquaires (donc les identifiants et mots de passes, carte bancaire etc) et qui les envoie sur une boite mail intracabe ou autre.

Avoir acces physique direct au pc c'est la maniere la plus puissante pour le hacking.


# IV- Bonus 👀




