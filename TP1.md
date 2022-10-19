### *19/10/2022*

### *Ce que j'ai fait pendant la séance:*

# TP DNS DHCP

__1.Trouvez l’adresse réseau, broadcast, masque sous-réseau, nombre de client possible, plages des clients possibles sur les réseaux suivants :__

--> ```192.168.0.0/24```
adresse réseau : 192.168.0.0

Broadcast Address:	192.168.0.255

Subnet Mask:	255.255.255.0

nombres de clients possibles: (class C)Hosts/Net: 254  

plages de clients possibles: 
HostMin:   192.168.0.1 
HostMax:   192.168.0.254 

--> ```10.0.0.0/8 ```

adresse réseau: 10.0.0.0

Broadcast Address:	10.255.255.255

Subnet Mask:	255.0.0.0

nombres de clients possibles: (class A) 16,777,214

plages de clients possibles:
HostMin:   10.0.0.1
HostMax:   10.255.255.254

--> ```172.16.0.0/255.255.0.0```

adresse réseau: 172.16.0.0

Broadcast Address:	172.16.255.255

Subnet Mask:	255.255.0.0

nombres de clients possibles: (class B) 65,534

plages de clients possibles:
HostMin:   172.16.0.1
HostMax:   172.16.255.254 

--> ```192.168.255.0/30```

adresse réseau: 192.168.255.0 

Broadcast: 192.168.255.3 

Netmask:   255.255.255.252 = 30

nombres de clients possibles:(class C) 2

plages de clients possibles:
HostMin:   192.168.255.1
HostMax:   192.168.255.2

--> ```10.50.0.0/22```
adresse réseau :10.50.0.0

Broadcast Address:	10.50.3.255

Subnet Mask:	255.255.252.0

nombres de clients possibles: (class B) 1,022

plages de clients possibles:
HostMin:   10.50.0.1
HostMax:   10.50.3.254 

--> ```172.28.0.0/255.248.0.0```

adresse réseau: 172.28.0.0

Broadcast Address:	172.31.255.255

Subnet Mask:	255.248.0.0

nombres de clients possibles: (class A) 524,286

plages de clients possibles:
HostMin:   172.24.0.1
HostMax:   172.31.255.254 

__2. Mise en place d’un serveur DHCP et DNS :__
__2.1. Prérequis :__

Dû à quelques problèmes techniques je n'ai pu lancer que 3 VMs sur les 4 initialement demandé (la VM-client_02 manquante)
 
-configuration des cartes réseaux des VMs
-désactivation de root
-interaction avec le firewall
-authentification par clé RSA

__2.3. Mettre en place une architecture DHCP selon les critères suivants (fin du TP non terminé)__

### *Ce que je compte faire à la séance prochaine:*

A la prochaine séance, début des recherches du projet de semestre 1 --> Projet Infra-Dev : Scripting Bash/Powershell sur USB (Goose Pranker)


