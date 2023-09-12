# Réseaux pour l'ingénierie

## Pre-read

Les notes de cours suivantes sont pour le cours GLO-2000. Seulement les informations pertinentes à l'examen sont inscrites.

### Mots clés

**H: Host**\
**WAN: Wide area network**\
**LAN: Local Area Network**\
**G: Gateway**\
**PAN: Personal Area Network**

### Schéma

Plusieurs réseaux doivent être connectés par WAN. Ils ne sont pas directement connectés, puisqu'ils doient avoir des équipements spéciaux, plus spécifiquement des G (autrement dit, des **Gateways**). Plusieurs WAN sont connnectés par un gateway. C'est une sorte de passerelle entre différents réseaux. Ces réseaux peuvent être des **LAN**s.

LAN1 + H1   ->  WAN1 + noeuds qui échangent des informations -> **GATEWAY** <-  WAN2 + noeuds   <-  LAN2 + H2

Soit le noeud 2 reçoit de l'information du noeud 1. S'il y a un problème, il y a soit une retransmission soit faire des calculs. Sinon, le noeud 2 renvoit de l'information confirmant le succès de la transmission du noeud 1.

## Chapitre 1: Introduction

### Définition d'un réseau

De façon générale. un réseau de communications est un ensemble d'équipements de télécommunications reliés entre eux (d'une certaine façon), permettant de véhiculer des données, de la voix, des images, … entre utilisateurs géographiquement éloignés (de quelques dizaines de mètres à plusieurs milliers de kilomètres).

![Schéma général de réseau](/schema_general.png)

### Caractérisation des liaisons
- Selon le nombre d'équipements
    - Liaisons point-à-point/peer to peer.
    - Liaison multipoint (sous réseau de communication, réseau local).
- Selon le mode d'exploitation
    - Liasion unidirectionnelle (simplex, exemple: la radio traditionelle).
    - Liaison bi-directionnelle en alternance (half-duplex, exemple: WiFi).
    - Liaison bi-directionnelle simultanée (full-duplex).

### Caractristiques physiques des réseaux
- Deux caractéristiques importantes:
    - Techniques de transmission:
        - La diffusion (broadcast): un seul canal est partagé par toutes les machines.
            - Un paquet (petit message) est envoyé, tous les autres le reçoivent.
            - la diffusion peut être générale ou restreinte
            - En général, les réseaux de petite taille utilisent la diffusion.
        - Le point à point: un canal est partagé par deux machines:
            - Un paquet peut passer par plusieurs machines intermédiaires avant d'atteindre sa destination (besoin de routage).
            - Une machine ne reçoit pas forcément tous les paquets des autres.
            - __En général__, les réseaux de grande taille utilisent le point à point.
    - La taille (étendue) du réseau:
    ![Schéma général de réseau](/taille_reseau.png)
        - Réseau personnel **PAN**.
        - Réseau locaux.
            - Étendue = une salle, un immeuble.
            - Topologie simple: Bus (exemple: Ethernet = norme IEEE 802.3) ou anneau (exemple: anneau à jeton = norme 802.5).
            - Généralement privés
            - Problm̀e de partage du canal
            - Access point ou Ethernet

