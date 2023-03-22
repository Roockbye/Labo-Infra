# Infrastructure compromise par Rubber Ducky 🐥

## 📁   __Compte-rendu de la journée (22/03/2023):__

### ✏️ __Ce qu'on à fait durant la séance:__

- Sur notre machine avec le windows serveur 2019 notre clé rubber ducky est détecté, nous avons donc réinstallé la machine avec un serveur windows 2016 puis nous l'avons promue en Domain Controller et nous avons mis en place l'Active Directory simple.
Quelques soucis ont eu lui au départ car nous avons constater que le Wifi n'était pas installé de base donc nous l'avons fait puis magré ca nous avons eu des problèmes pour activer tout de meme le Wifi, ce dernier restait en desactivé

- Installation réussi cette fois sur notre deuxième machine, client cette fois de Windows 10

- Pour finir la dernière fois nous avons eu quelques problèmes pour apprendre à comprendre comment fonctionnait la rubber ducky, car les scripts ne fonctionnaient pas. Nous avons finit par comprendre que c'est parce que le script prenait en clavier US alors que nous possédons des claviers fr, ce qui faisait que tout les scripts échouait. Nous avons pu donc résoudre ce problème et réussir à faire un script de base( print Hello World). 

### ⏰ __Ce qu'on va faire à la prochaine séance:__

- Relier le client au Active Directory Simple de notre serveur

- Avancer sur la recherche du script de la Rubber Ducky qui doit recuperer les infos de l'infrastructure

- Installer une back door de notre choix sur le client