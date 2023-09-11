# Réseaux pour l'ingénierie

## Introduction

### Schéma

**H: Host**
**WAN: Wide area network**
**LAN: Local Area Network**
**G: Gateway**

Plusieurs réseaux doivent être connectés par WAN. Ils ne sont pas directement connectés, puisqu'ils doient avoir des équipements spéciaux, plus spécifiquement des G (autrement dit, des **Gateways**). Plusieurs WAN sont connnectés par un gateway. C'est une sorte de passerelle entre différents réseaux. Ces réseaux peuvent être des **LAN**s.

|       LAN1    |       |   WAN1                |                       |   WAN2    |       |   LAN2    |
|               |   ->  |   noeuds qui échangent|   ->  **GATEWAY** <-  |   noeuds  |   <-  |           |
|               |       |    des informations   |                       |           |       |           |
|       H1      |       |                       |                       |           |       |   H2      |

Soit le noeud 2 reçoit de l'information du noeud 1. S'il y a un problème, il y a soit une retransmission soit faire des calculs. Sinon, le noeud 2 renvoit de l'information confirmant le succès de la transmission du noeud 1.

### Plan de cours
