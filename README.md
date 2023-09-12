# Réseaux pour l'ingénierie

## Pre-read

Les notes de cours suivantes sont pour le cours GLO-2000. Seulement les informations pertinentes à l'examen sont inscrites.

### Mots clés

**H: Host**\
**WAN: Wide area network**\
**LAN: Local Area Network**\
**G: Gateway**\
**PAN: Personal Area Network**\
**MAN: Réseaux métropolitains**

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
            - **En général**, les réseaux de grande taille utilisent le point à point.
    - La taille (étendue) du réseau:
    ![Schéma général de réseau](/taille_reseau.png)
        - Réseau personnel **PAN**
        - Réseau locaux:
            - Étendue = une salle, un immeuble.
            - Topologie simple: Bus (exemple: Ethernet = norme IEEE 802.3) ou anneau (exemple: anneau à jeton = norme 802.5).
            - Généralement privés.
            - Problm̀e de partage du canal.
            - Access point ou Ethernet.

**Remarque**\
Sans fil ne veut pas nécessairement dire mobile. Les utilisateurs sont mobiles, mais pas l'équipement.

- Réseaux métropolitains (MAN)
    - Étendue = une ville
    - Peut être privé ou public
    - Pas d'éléments de commutation (routage) -> simple
    - Norme spéciale IEEE-802.6
- Réseaux longue distance (WAN)\
    **n: nombre de noeuds**\
    **m: nombre de liaisons**\
    **m = f(n)**
    - Étendue = une région, un continent.
    - Sous-réseau de commutation: Ensemble de commutateurs reliés entre eux.
    - Un commutateur (ordinateur): ordinateur spécialisé qui permet d'acheminer des paquets.
    - Quelques topologies possibles d'un sous réseau:
        - Étoile (m = n-1, min = 2).
        - Anneau (m = n, min = 3).
        - Arbre (m = n-1, min = 2).
        - Maillage régulier (m = n * (n-1) / 2, min = 2).
        - Anneau-interconnecté (m = n+1, min = 5).
        - Maillage irrégulier (n-1 <= m <= n * (n-1) / 2)
- Interréseaux
    - Ensemble de réseaux interconnectés au moyen de machines appelées passerelles (gateways)
    > Ne pas confondre: internet et Internet (le bon est I majuscule)

