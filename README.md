# Réseaux pour l'ingénierie

## Pre-read

### Schéma

**H: Host**
**WAN: Wide area network**
**LAN: Local Area Network**
**G: Gateway**

Plusieurs réseaux doivent être connectés par WAN. Ils ne sont pas directement connectés, puisqu'ils doient avoir des équipements spéciaux, plus spécifiquement des G (autrement dit, des **Gateways**). Plusieurs WAN sont connnectés par un gateway. C'est une sorte de passerelle entre différents réseaux. Ces réseaux peuvent être des **LAN**s.

LAN1 + H1   ->  WAN1 + noeuds qui échangent des informations -> **GATEWAY** <-  WAN2 + noeuds   <-  LAN2 + H2

Soit le noeud 2 reçoit de l'information du noeud 1. S'il y a un problème, il y a soit une retransmission soit faire des calculs. Sinon, le noeud 2 renvoit de l'information confirmant le succès de la transmission du noeud 1.

## Chapitre 1: Introduction

### Définition d'un réseau

De façon générale. un réseau de communications est un ensemble d'équipements de télécommunications reliés entre eux (d'une certaine façon), permettant de véhiculer des données, de la voix, des images, … entre utilisateurs géographiquement éloignés (de quelques dizaines de mètres à plusieurs milliers de kilomètres).

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](/schema_general.png)

### Caractérisation des liaisons
- Selon le nombre d'équipements
    - Liaisons point-à-point/peer to peer
    - Liaison multipoint (sous réseau de communication, réseau local)
- Selon le mode d'exploitation
    - Liasion unidirectionnelle (simplex, exemple: la radio traditionelle)
    - Liaison bi-directionnelle en alternance (half-duplex, exemple: WiFi)
