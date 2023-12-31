# Réseaux pour l'ingénierie

##### Table des matières

[Pre-read](#pre-read)\
[Équations](#équations)\
[Division Binaire](#division-binaire)\
[Mots clés](#mots-clés)\
[Schéma](#schéma)
- [Section Théorique](#section-théorique)
    - [Chapitre 1: Introduction](#chapitre-1-introduction)
        - [Définition d'un réseau](#définition-dun-réseau)
        - [Caractérisation des liaisons](#caractérisation-des-liaisons)
        - [Caractristiques physiques des réseaux](#caractristiques-physiques-des-réseaux)
        - [Architectures logicielles](#architectures-logicielles)
        - [Types de services](#types-de-services)
        - [Modèles de référence et encapsulation](#modèles-de-référence-et-encapsulation)
        - [Architecture TCP/IP](#architecture-tcpip)
        - [Encapsulation](#encapsulation)
    - [Chapitre 2: Couche physique](#chapitre-2-couche-physique)
        - [Bases théoriques](#bases-théoriques)
        - [Couche physique](#couche-physique)
        - [Analyse de Fourier](#analyse-de-fourier)
        - [Limitations](#limitations)
        - [Limitations: bande passante](#limitations-bande-passante)
        - [Débit maximal](#débit-maximal)
    - [Chapitre 3: Couche liaison de données](#chapitre-3-couche-liaison-de-données)
        - [Fonctions de la couche Liaison de données](#fonctions-de-la-couche-liaison-de-données)
        - [Trame](#trame)
        - [Délimitation de trames](#délimitation-de-trames)
        - [Détection et correction d'erreurs](#détection-et-correction-derreurs)
        - [Contrôle de flux](#contrôle-de-flux)
        - [Partage du support physique](#partage-du-support-physique)
        - [Protocoles de liaison de données](#protocoles-de-liaison-de-données)
    - [Chapitre 4: MAC](#chapitre-4-MAC)
        - [Introduction](#introduction)
        - [Problèmes d'allocation d'un canal](#problèmes-dallocation-dun-canal)
        - [Couche liaison dans un LAN](#couche-liaison-dans-un-lan)
        - [Protocoles de Gestion d'accès](#protocoles-de-gestion-daccès)- [Normes IEEE 802 des LAN](#normes-ieee-802-des-lan)
        - [Les ponts](#les-ponts)
- [Section Pratique](#section-pratique)
    - [Protocoles](#protocoles)
        - [Protocole Ethernet II](#protocole-ethernet-ii)
        - [Protocole IP](#protocole-ip)
        - [Protocole ARP](#protocole-arp)
        - [Protocole TTL: Time to live](#protocole-ttl-time-to-live)
        - [Protocole ICMP](#protocole-icmp)
        - [Protocole DNS](#protocole-dns)

## Pre-read

Les notes de cours suivantes sont pour le cours GLO-2000. Seulement les informations pertinentes à l'examen sont inscrites.

### Équations

**% Données nettes** = Total Données nettes(TDN) / TDN + Total Header + Total Enqueue

### Division Binaire

1. Mettre le diviseur en dessous
2. Différent = 1, Même = 0
3. On continue

### Mots clés

**TDN: Total Données Nettes**\
**H: Host**\
**WAN: Wide area network**\
**LAN: Local Area Network**\
**G: Gateway**\
**PAN: Personal Area Network**\
**MAN: Réseaux métropolitains**\
**ETTD : Équipement Terminal de Transmission de Données**\
**ETCD : Équipement Terminal de Circuit de Données**

### Schéma

Plusieurs réseaux doivent être connectés par WAN. Ils ne sont pas directement connectés, puisqu'ils doient avoir des équipements spéciaux, plus spécifiquement des G (autrement dit, des **Gateways**). Plusieurs WAN sont connnectés par un gateway. C'est une sorte de passerelle entre différents réseaux. Ces réseaux peuvent être des **LAN**s.

LAN1 + H1   ->  WAN1 + noeuds qui échangent des informations -> **GATEWAY** <-  WAN2 + noeuds   <-  LAN2 + H2

Soit le noeud 2 reçoit de l'information du noeud 1. S'il y a un problème, il y a soit une retransmission soit faire des calculs. Sinon, le noeud 2 renvoit de l'information confirmant le succès de la transmission du noeud 1.

# Section Théorique
## Chapitre 1: Introduction

### Définition d'un réseau

De façon générale. un réseau de communications est un ensemble d'équipements de télécommunications reliés entre eux (d'une certaine façon), permettant de véhiculer des données, de la voix, des images, … entre utilisateurs géographiquement éloignés (de quelques dizaines de mètres à plusieurs milliers de kilomètres).

![Schéma général de réseau](/images/ch1/schema_general.png)

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
    ![Schéma général de réseau](/images/ch1/taille_reseau.png)
        - Réseau personnel **PAN**
        - Réseau locaux:
            - Étendue = une salle, un immeuble.
            - Topologie simple: Bus (exemple: Ethernet = norme IEEE 802.3) ou anneau (exemple: anneau à jeton = norme 802.5).
            - Généralement privés.
            - Problm̀e de partage du canal.
            - Access point ou Ethernet.

**Remarque**
> Sans fil ne veut pas nécessairement dire mobile. Les utilisateurs sont mobiles, mais pas l'équipement.

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

### Architectures logicielles
- Réseau: matériels + logiciels.
- Logiciel: On a besoin d'implanter un grand nombre de fonctions (détection et correction d'erreurs, contrôle de flux, routage, etc.) pour pouvoir communiquer convenablement.
- Problème: les fonctions à implanter sont nombreuses et complexes.
- Quoi faire?: regrouper les fonctions en modules (diviser pour régner)-> réduire un problème complexe en plusieurs petits problèmes.
- Comment faire le découpage?: utiliser les techniques de génie logiciel (couplage, modularité. encapsulation, etc.)
- Résultat du découpage:
    - Plusieurs couches
        - Couches de bas niveau: pour transmission et acheminement des informations;
        - Couches intermédiaires: pour gestion des communications et des ressources nécessaires aux échanges;
        - Couches de haut niveau: pour exécution des commandes, formatage et affichage des informations.
    - Une couche = un niveau d'abstraction
    - Une couche n utilise les **services** de la couche n-1 et ses propres moyens pour offrir des services plus appropriés à la couche n+1
    - Relations entre les couches n et n+1
        - n: utilisateur des services.
        - n-1: fournisseur des services
    - Nombre/nom/fonction des couches varie selon le réseau.
- Protocole : Ensemble de règles et des conventions décrivant la
syntaxe et la sémantique des messages échangés et la façon
dont la transmission se déroule.
    - Syntaxe
        - Les différents champs qu'on trouve dans chaque message
        - Le nombre de bits occupé par chaque champ
    - Sémantique: la signification de chaque champ
- Chaque couche utilise ses propres protocoles pour communiquer
avec son homologue (entités homologues).
- Aucune donnée n’est transférée directement de la couche n
(n>1) d’une machine à la couche n d’une autre machine.
- Pour que la couche n+1 puisse utiliser la couche n,
elle doit connaître l’interface de cette dernière.
- Une interface définit les opérations élémentaires et
les services qu’une couche inférieure offre à sa
supérieure.
- Architecture d’un réseau = ensemble de couches et
de protocoles.
> Remarque: La spécification d’une architecture doit contenir
suffisamment d’information pour permettre l’écriture de
programmes et la construction de matériels de chaque
couche.

|||
| ------------- | ------------- |
| ![](/images/ch1/img41.png)  | ![](/images/ch1/img42.png) |



Il est important de comprendre la différence entre la **communication virtuelle** et la **communcation effective**
- Les processus pairs de la couche N conçoivent leur communication de façon horizontale grâce au protocole de la couche N ➔ une communication virtuelle.
- La communication effective se fait avec les couches inférieures par l’interface.

![](/images/ch1/img43.png)

- Couche 4: Encapsulation d'un **header** (entête) et du message de la couche 5.
- Couche 3: découpage de l'information en deux différents messages
- Couche 2: même concept qu'à la couche 3 avec un trailer (**T**)
- Couche 1: décapsulation

### Types de services
- Service avec connexion
    - Modélisé d'après le système de téléphone
    - Principe: trois étapes
        - Établir la connexion.
        - Utiliser la connexion.
        - Liberer la connexion.
    - Avantages:
        - Négociation au moment de la connexion (transfert fiable, régularisation de flux d'information, etc.)
        - Minimisation de flux d'information de contrôle
    - Inconvénients: 
        - Procédures lourdes d'établissement et de libération de connexions.
- Services sans connexion
    - Modélisé d'après le système postal.
    -Principes:
        - Pas besoin d'établir une connexion pour envoyer des données
        - Chaque message contient l'adresse de destination
        - Chaque message est acheminé indépendamment des autres.
    - Avantages:
        - Négociation plus facile
    - Inconvénients
        - Perte, duplication, déséquencements possibles.
- Les services sont caractérisés par des niveaux de qualité
de service
    - Fiable (reliable):
        - Principe:
            - Utilise des techniques de détection ou de correction d'erreurs
            - Envoyer des accusés de réception pour confirmer que le message est bien reçu
        - Inconvénients
            - Surcharge et délais
        - Exemple d'utilisation: transfert de fichiers
    - Non fiable (unreliable): appelé aussi service datagramme.
        - Principe: pas d’accusé de réception et pas de détection d’erreurs.
        - Exemple d’utilisation: envoi électronique de messages publicitaires.

### Modèles de référence et encapsulation
**Normalisation**

Qu’est ce qu’une norme?: Des accords documentés décrivant
des spécifications des produits ou des services.
- Exemple: format d’une carte bancaire (longueur, largeur,
épaisseur, position de la bande magnétique, etc.).
- Pourquoi une norme?: Éliminer les incompatibilités entre les
produits et les services.
- Si on ne parle pas le même « langage », alors comment peut-on communiquer et se comprendre?
- Qui définit les normes?: des organismes nationaux (SCC « Standards Council of Canada », AFNOR « France », ANSI « USA ») et internationaux (ISO « International Organization for
Standardization »).

**Modèle de référence OSI (Open Systems Interconnection)**

- L’objectif de OSI est de définir
une standardisation des règles
d’interaction entre les systèmes
interconnectés.
- OSI ne s’intéresse qu’au
comportement externe, le
fonctionnement interne ne
présente aucun intérêt pour
OSI.
- Élaboré par ISO et comporte 7
couches.

![](/images/ch1/OSI.png)

- Couche physique: transmission de bits sur un canal de communication.
    - Cette couche spécifie les caractéristiques physiques propres à la transmission du signal.
    - Entre autres, elle répond aux questions:
        - Quelle tension représente < 1 >?
        - Combien de temps dure un bit?
        - Combien de broches a un connecteur?
        - Combien de câbles le média a-t-il?
    - Exemples de protocoles: RS-232, V.24, V.35, X.21, etc.
- Couche liaison de données:
    - Une échange de trames (série de bits) entre deux machines voisines, et ce, sans erreur, ni duplication, ni perte
        - un formattage des données,
        - un contrôle d'erreurs,
    - Une gestion de flux: éviter que l'émetteur envoie plus que le récepteur ne peut traîter (émetteur rapide, récepteur lent).
    - Un partage de support physique entre plusieurs stations.
    - Exemples des protocoles: HDLC (High-level Data Link Control), LAPB (Link Access Procedure Balanced), LAPD (Link Access Procedure on the D channel), SDLC (Synchronous Data Link Control), PPP (Point-to-Point Protocol), LAP (Link Access Procedure), etc.
- Couche réseau:
    - Acheminement des paquets de la source à la destination.
    - Routage: acheminer les paquets d’informations
    vers leur destination au travers du maillage des
    nœuds de commutation.
    - Contrôle de congestion: éviter les embouteillages
    de paquets dans le réseau.
    - Exemples de protocoles: X.25, IP (Internet Protocol), etc.
- Couche transport:
    - Transport des données de bout en bout.
        - Abstraction vis-à-vis du réseau réel
        - Vérification de réception des segments
        - Vérification de l'ordre de réception des segments
        - Exemples de protocoles: TCP (Transmission Control Protocol), UDP (User Datagram Protocol), etc.
- Couche session:
    - Établir des sessions de communication entre machines
    - Gérer et organiser des dialogues.
    - Exemples de protocoles: X.225, X.245, ASN.1 (Abstract Syntax Notation One), etc.
- Couche présentation:
    - Elle fournit le mécanisme (codage
    ou présentation de l’information) permettant de présenter des données de façon à ce qu’elles soient comprises par l’application émettrice et par l’application réceptrice.
        - Cette couche s’intéresse à la syntaxe et la sémantique de l’information transmise.
        - Elle gère les conversions de code, les compressions, les encryptages.
        - Exemples de protocoles: XDR (External Data Representation), ASN.1 (Abstract Syntax Notation One), etc.
- Couche application:
    - Les protocoles de cette couche
    servent directement l’utilisateur final en fournissant un ensemble de services standards : messagerie électronique, transfert de fichiers, etc.
    - Exemples de protocoles: FTP (File Transfer Protocol), SMTP (Simple Mail Transfer Protocol), SNMP (Simple Network Management Protocol), etc.

![](/images/ch1/OSI2.png)

### Architecture TCP/IP

- Architecture définie par la défense américaine (DoD).
- Le but est la connexion de plusieurs réseaux utilisant
des protocoles de communication différents et incompatibles.

> IMPORTANT! La couche de présentation et la couche de session sont fusionnées dans la couche application pour TCP/IP. Elles ne sont donc pas présentes dans le modèle.

![](/images/ch1/TCPIP2.png)
![](/images/ch1/TCPIP.png)

### Encapsulation
- Au niveau liaison
    ![](/images/ch1/entetetcpip.png)
    - Trame: Adresse physique (MAC)
    - Paquet: Adresse réseau/logique (IP)

## Chapitre 2: Couche physique

### Bases théoriques

**Éléments de transport d'information**

![](/images/ch2/transportinfo.png)
- ETTD : Équipement Terminal
de Transmission de Données
    - Exemple: ordinateur
- ETCD : Équipement Terminal
de Circuit de Données
    - Exemple: modem
- Support ou canal de
transmission :
    - Exemple:Coaxial, Fibre optique ...

![](/images/ch2/exempletransportinfo.png)

#### Exemple d'accès à internet

![](/images/ch2/Screenshot%20from%202023-09-25%2019-00-34.png)

### Couche physique

- La couche physique est la couche la plus basse du modèle OSI. Elle est censée définir les moyens:
    1. mécaniques;
    2. électriques;
    3. fonctionnels.

    Permettant:
    1. d'établir;
    2. de maintenir;
    3. et de libérer
    
    Une connexion entre un ETTD et un ETCD.

### Analyse de Fourier

- Théorème: Toute fonction g(t) périodique de période T peut être décomposée de la manière suivante:

    ![](/images/ch2/fourier.png)

    - f=1/T: fréquence fondamentale (de base)
    - an, bn: amplitudes harmoniques

- Exemple: signal rectangulaire
    
    ![](/images/ch2/rectangulaire.png)
    - n: nombre d'harmoniques

- Transmission du caractère b codé en ASCII (01100010)

    ![](/images/ch2/Screenshot%20from%202023-09-25%2019-17-06.png)

### Limitations

- L’analyse de Fourrier permet de comprendre les origines de certaines perturbations de signaux durant leur transmission.
    - Limitation du canal de transmission: incapable de trasmettre toutes les harmoniques -> déformation du signal.
    - Distortion temporelle: toutes les composantes harmoniques d'un signal ne se propagent pas à la même vitesse.
- Autres limitations
    - Atténuation: correspond à une perte d'énergie du signal lors de sa propagation.
    - Bruit: des signaux indésirables qui s'ajoutent au signal transmis.

### Limitations: bande passante

- Bande passante d'un support: c'est la gramme de fréquences transmises sans affaiblissement par un support de trasmission. Si [f1, f2] est la bande passante, alors la largeur de bande est W = f2-f1.

- Observations:
    - On suppose qu'on envoie  un caractère avec une vitesse de b bit/s. On suppose également qu'on envoie le mête caractère plusieurs fois (T = 8*Tb avec Tb = durée d'un bit).
    - T = 8*Tb = 8/b secondes -> fréquence de base f = f1 = 1/T = b/8 Hz et fn = nf1
    - Nombre d'harmoniques = W/f
    - Si on utilise une ligne téléphonique qui ne laisse passer que les fréquences entre 300 et 3400 Hz, on aura les résultats:
    
        ![](/images/ch2/results.png)

>Remarques
>- Il y a un lien direct entre le débit et la bande passante -> il y a une limitation.
>- À partir de la vitesse 38 400bps, on aura aucune chance de reconstruire le signal
>- Si on envoie la séquence 10101010... (le pire scénario), on aura T=2*Tb.
>- Si T (up) alors f (down) et, dans ce cas, on aura besoin d’une bande passante moins large.

### Débit maximal

- Amélioration du débit
    - Utiliser plusieurs niveaux du signal
        - Exemple (V1, V2, V3, V4): V1 -> 00; V2 -> 01; V3 -> 10; V4 -> 11
        > Remarques:
        > - Baud = le nombre maximal de transitions par unité de temps.
        > - Débit = le nombre de bits enovyés par seconde
- Rapidité de modulation
    - Rm = 1/2Tb bauds
    - Débit = Rm * log2(V) bits/s
    - V: Valence du signal (nombre de niveaux)
    - V = 2 exposant p
    - p = nombre de bits par niveau
    - D = Rm * p
- Débit maximal:
    - Théorème de Nyquist:
        - Hypothèse: le signal n'est affecté par aucun bruit.
        - Débit maximal = **2 H Log2(V)**
            - la largeur de bande
            - V: nombre de niveaux du signal
    - Théorème de Shannon:
        - En présence de bruit, le débit maximal est donné par la formule:
            - Débit maximal = **Log2(1+S/R)**
                - S: puissance du signal
                - R: puissance du bruit
    - Conversion Decibels (dB):
        - dB = 10 log10 (S/R)
        - S: puissance du signal
        - R: puissance du bruit

### Techniques de transmission

- Encodage de données (Transmission en bande de base)
    - Code tout ou rien: 0 -> -V; 1 -> +V
    - Code NRZ (Non Return to Zero): 0 -> -V; 1 -> +V
    - Code bipolaire: 0 -> 0; 1 -> +V ou -V
    - Code RZ (Return to Zero): 0 -> -V; 1 -> +V
    - Code Manchester: 0 -> -V; 1 -> +V
    - Code Miller: 0 -> -V; 1 -> +V

- Modulation: Modifier (moduler) un ou plusieurs paramètres d'une onde porteuse en fonction du rythme des signaux binaires à transmettre.
    - Porteuse: Vp(t) = Ap cos(2pifpt + 0p)
    - Paramètres de la porteuse: Ap, fp, et 0p
    - 4 types de modulation:
        - Modulation d'amplitude (modifier Ap)
        - Modulation de fréquence (modifier fp)
        - Modulation de phase (modifier 0p)
        - Modulation combinée (modifier plusieurs paramètres à la fois)
    - 0 = 2pi / V

    ![](/images/ch2/transmission.png)

### Modes de transmission

- Unidirectionnelles (simplex): Les données sont transmises dans une seule direction. Exemple: radio, télévision.
- Bidirectionnelles en alternance (half-duplex): Les données sont transmises dans les deux directions, mais pas simultanément. Exemple: radio amateur, radio de police.
- Bidirectionnelles simultanées (full-duplex): Les données sont transmises dans les deux directions simultanément. Exemple: téléphone, réseau téléphonique.
- Série: les bits sont transmis un à la fois sur un seul fil.
- Parallèle: les bits sont transmis simultanément sur plusieurs fils.

### Commutation de circuits

- Caractéristiques
    - Utilisation exclusive du chemin après connexion.
    - Monopole des liaisons composant le chemin
    - libération des liaisons après l'échange (déconnexion)
- Avantages
    - livraison séquentielle des messages
- Inconvénients
    - Mal adaptée au transports de données

### Commutation de messages

- Aucun chemin n'est préalablement établi entre l'émetteur et le récepteur.

- Le message transite d'un noeud à l'autre où il est inspecté, puis gardé en mémoire jusqu'à ce qu'une liaison vers le prochain noeud se libère, d'où son appelation _store_ and _forward_

![](/images/ch2/Screenshot%20from%202023-09-25%2020-59-11.png)

- Caractéristiques
    - Contrôle d'erreur à chaque noeud
    - Pas de monopole de chemin
    - Acheminement par étape du message au complet
- Avantages
    - Meilleure utilisation des liaisons et des ressources du réseau
- Inconvénients
    - Nécessité de grandes capacités de mémoire aux noeuds
    - Possibilité de saturation des liaisons par des messages de grande taille
    - Pénalisation des messages courts

## Couche liaison de données
_Au niveau du WAN_
### Fonctions de la couche Liaison de données
Cette couche permet essentiellement:

- Le formatage des données
    - le flot de bits entrant doit être segmenté en trames.
    - le début et la fin de chaque bloc doivent être clairement identifiés
- Le contrôle des erreurs: Le protocole doit fournir:
    - Une technique permettant la détection des erreurs.
    - La possibilité de retransmission des trames dans le cas ou les erreurs ne peuvent pas être corrigées.
- Le contrôle de flux: Le protocole doit fournir des mécanismes pour s'assurer que l'émetteur ne transmette pas plus vite que ce que peut absorber le récepteur.
- Partage du support physique

### Trame
- Le flot de bits entrant doit être segmenté en blocs appelés trames.
- Pourquoi?
    - Si une erreur se produit lors de la transmission, l'unité de retransmission sera la trame (au lieu de retransmettre toute
    l’information, on renvoie simplement une trame).
- Problème: Comment alors délimiter une trame?

### Délimitation de trames
- Compter les caractères: Ajouter un caractère dans l'en-tête d'une trame indiquant le nombre de caractères qu'elle contient.
    - **Inconvénient:** Si, lors de la transmission, une erreur se produit dans le champ indiquant le nombre de caractères, le récepteur ne serait plus capable de délimiter correctement les trames.
- Ajouter des caractères de début de trame, de fin de trame et de transparence
    - Début de trame = DLE STX (Data Link Escape, Start of Text)
    - Fin de trame = DLE ETX (Data Link Escape, End of Text)
    - Pour éviter que la séquence DLE STX ou DLE ETX ne se
    retrouve parmi les données à envoyer, on ajoute un caractère DLE devant tout caractère DLE apparaissant dans les données à transmettre.
    - **Inconvénient:** Les séquence de bits associées aux délimiteurs de trames dépendent du mécanisme de codage de caractère utilisé.
- Utiliser des fanions et des bits de transparence:
    - début de trame = 01111110 (fanion)
    - fin de trame = 01111110 (fanion)
    
    - Pour évtier qu'un fanion ne se retrouve parmi les données à envoyer. Plus précisément, on insère un bit de 0 après chaque séquence de 5 bits de 1 consécutifs.

### Détection et correction d'erreurs

- Erreur de transmission: i {1,2, …}| âi – ai  0.
- Taux d’erreur binaire : Le nombre de bits erronés sur le nombre total de bits reçus pendant un intervalle de temps.
- Les codes détecteurs:
    - Détecter des erreurs
    - Ajouter aux données transmises des informations de contrôle
    - Une fois qu'une erreur est détectée, on demande la retransmission de la trame erronée.
- Détection par parité verticale (VRC: Vertical Redundancy Check):
    - Information utile = b1.b2....bn
    - Contrôle
        - Parité paire = 0, si b1 + b2 + ... + bn est pair (1 sinon)
        - Parité impaire = 0, si b1 + b2 + ... + bn est impair (1 sinon)
    - Information de contrôle = 1 bit
    - Cette méthode permet de détecter des blocs qui contiennent un nombre impair de bits éronnés
    - Si les erreurs se produisent en rafales (un bloc peut comporter plusieurs bits éronnés), il y aura une chance sur 2 que cette erreur soit détectée.
- Détection par parité longitudinale (LRC: Longitudinal Redundancy Check)
    - Regrouper les données sous forme de blocs pour effectuer un codage VRC pair selon les lignes et les colonnes.
    - Message à envoyer:
        - HELLO! = 01001000 01000101 01001100 01001100 01001111 00100001
    - Message transmis: 10010000 10001011 10011001 10011001 10011111 01000010 11000110
    - Cette méthode permet de détecter toutes les erreurs simples, doubles ou triples.
- Détection par code cyclique (CRC: Cyclic Redundancy Check)
    - Connu aussi sous le nom de codes polynomiaux.
    - Principe:
        - L'émetteur et le récepteur se mettent d'accord sur un diviseur. Exemple: 
        - Information de contrôle = le reste de la division de message sur diviseur
            - Message 57268
            - Contrôle = Reste(57268/84) = 64
            - Message transmis 5726864

![](/images/ch3/Screenshot%202023-10-02%20at%2019-47-54%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)

- CRC (méthode alternative)
    - Avant la communication:
        - Pour un message de k bits, l’émetteur et le récepteur se
        mettent d’accord sur un polynôme générateur G(x) de degré r
        tel que r <= k - 1.
- Algorithme:
    - Ajouter r bits « 0 » au message M pour former M’. M’ contient
    (k + r) bits.
    - Effectuer la division binaire (M’/G). Le CRC correspond au
    reste de cette division.
    - Ajouter les bits du CRC à M pour former un nouveau message T.
    - Soit T’ le message reçu. À la réception, si le reste de la division
    binaire (T’/G) est non nul, il y a erreurs de transmission.

### Protocoles élémentaires

- Envoyer et attendre (Stop and Wait):
    - Hypothèses:
        - Les données utiles circulent dans un seul sens
        - Les trames envoyées contiennent l'information nécessaire (CRC par exemple) pour que le récepteur puisse détecter les erreurs éventuelles
    - Côté récepteur:
        - Si la trame reçue ne contient pas d'erreur, il envoie un message d'acquittement (ACK) à l'émetteur.
        - Si la trame reçue contient une erreur, il n'envoie rien à l'émetteur.
    - Côté émetteur:
        - Il envoie une trame et il attend une durée de temps fixe t (timeout) (t >= au temps requis pour qu'une trame fasse un aller retour).
        - Si au bout de t unité de temps, il ne reçoit pas un acquittement ACK, il retransmet la trame.
    - Avantages:
        - Simplicité: Facile à comprendre et à implanter.
        - Il ne demande pas beaucoup de mémoire : Le récepteur
        utilise un tampon qui peut contenir une seule trame.
        - Contrôle de flux : L’émetteur n’envoie pas plus que ce
        que le récepteur peut traiter. Il envoie une trame et il
        s’assure qu’elle a été traitée par le récepteur avant
        d’envoyer la suivante.
    - Inconvénients :
        - Les données utiles circulent dans un seul sens.
        - Le canal de transmission n’est pas exploité comme il faut.
        Durant à peu près la moitié du temps, l’émetteur chôme.

![](/images/ch3/Screenshot%202023-10-02%20at%2020-32-20%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)

#### Problème:
Si l'acquittement d'une trame(n) est perdu, l'émetteur va la retransmettre, mais le récepteur va la considérer comme une nouvelle trame (n+1) et va l'accepter. On aura donc deux trames identiques.

#### Solution: 
Il suffit de numéroter les trames pour résoudre le problème précédent. À cette fin, on va ajouter un champ dans l'en-tête de chaque trame pour mettre leurs numéros. 

> La seule ambiguïté du coté de
récepteur est de savoir s’il s’agit de la trame
précédente ou d’une nouvelle trame, donc un
seul bit suffira pour la numérotation des
trames. La première trame porte le numéro 0,
la deuxième 1, la troisième 0, la quatrième 1,
etc. 

![](/images/ch3/Screenshot%202023-10-02%20at%2020-36-34%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)

#### Robustesse
Avec le protocole précédent, si l'émetteur ne règle pas convenablement son temporisateur (plus petit que la valeur convenable), il y aura la possibilité que le récepteur rejette des trames en les croyant des retransmissions

![](/images/ch3/Screenshot%202023-10-02%20at%2020-39-57%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)

#### Protocole plus robuste:
On veut
un protocole qui fonctionne
convenablement même si
l’émetteur ne règle pas
convenablement son
temporisateur.

#### Solution:
Numéroter les acquittements

![](/images/ch3/Screenshot%202023-10-02%20at%2020-43-48%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)

#### Rejet sélectif

- Cette stratégie consiste à ignorer seulement les
trames erronées.

- Les trames correctement reçues après une
erreur seront toutes stockées

- Une fois, la trame erronée est retransmise, la
couche liaison réceptrice remet les paquets à
sa couche supérieure dans le bon ordre.

Go back N : W <= 2^m - 1

Rejet Sélectif : W <= 2^(m-1)

#### Exemple de protocole de couche de liaison

- HDLC (High-Level Data Link Control)
    - IBM développe le protocole SDLC (Synchronous
    Data Link Control), l’utilise dans SNA et le
    propose à l’ANSI comme norme pour les Etats-
    Unis et à l’ISO comme norme internationale.
    - L’ANSI a adopté ADCCP (Advanced Data
    Communication Control Protocol)
    - ISO a adopté HDLC
    - CCITT de sa part adopte LAP (Link Access
    Procedure) issue de HDLC
    - Structure de trame HDLC
        ![](/images/ch3/Screenshot%202023-10-16%20at%2019-02-08%20Présentation%20PowerPoint%20-%20Liaison_A2023.pdf.png)
    - Trame d'information
        - Trame transportant de l’information
    - Trame de supervision
        - Trame qui gère l’acquittement, le contrôle de flux et
        indiquant l’état de la disponibilité de la station.
        - Pas de champ « DONNÉES ».
    - Trame non numérotée
        - Trame dotée de fonctions complémentaires (initialisation,
        libération, …)
        - En général, pas de champ « DONNÉES ».

## Chapitre 4: MAC
_Contrôle d'accès au canal_
### Introduction
#### Ce chapitre
_Ligne partagée par plusieurs utilisateurs_
#### Problème/enjeu de se chapitre
_Éviter les collisions_
#### Constituants d'un LAN
- Câblage d'interconnexion des noeuds;
- Méthode d'accès pour assurer le partage de support de transmission;
- Méthode d'adressage pour l'identification des noeuds;
- Ensemble de protocoles pour permettre la communication;
- Système d'exploitation réseau pour contrôler l'utilisation des périphériques distants;
- Programmes utilisant les ressources mises en commun.

### Problème d'allocation d'un canal
#### Allocation dynamique
- Principe:
    - Un seul canal logique de communication est disponible pour toutes les communications.
    - Lorsqu'une station a de l'information, elle l'envoie, sans se préoccuper des autres usagers.
- S'il y a collision, les signaux seront retransmis ultérieurement.
    - Avantages: 
        - Ne nécessite aucune synchronisation
        - Complètement décentralisée
    - Inconvénients:
        - Perte de l'information en cas de collision
        - Lorsque le nombre d'utilisateurs augmente, le débit du système de vient plus faible.

### Couche liaison dans un LAN
- LLC: Logical Link Control
- MAC: Medium Access Control

![](/images/ch4/Screenshot_20231106_185055.png)

### Protocoles de Gestion d'accès
#### MAC
Trois stratégies:
1. La contention:
    - une station émet quand elle veut.
    - si collision -> Entreprendre une action.
    - Utilisée par "Contention Systems" (systèmes qui partagent un canal selon une méthode qui peut conduire à des conflits).
2. Technique Round-Robin:
    - Chaque station attend son tour avant d'émettre en cycle.
    - Utilisée par les Token-Based systems.
3. Technique de réservation
    - Demander la permission (de réserver le canal) avant d'émettre.
    - Utilisée par les Slotted systems.

#### Les protocoles CSMA (Carrier Sense Multiple Access)
- Principe:
    - Avant d'envoyer, s'assurer que le canal est libre (écouter le canal)
- 1-persistant:
    - si le canal est **occupé**, alors rester à l'écoute jusqu'à ce qu'il devienne libre
- non-persistant:
    - si le canal est **occupé**, alors attendre un temps aléatoire puis réécouter
- p-persistant:
    - si le canal est **libre**, alors envoyer avec une probabilité (0 <= p <= 1)
##### CSMA avec détection de collision (CSMA/CD)
- Fonctionnement: écouter le canal et arrêter la transmission dès qu'une collision est détectée.
- Principe:
    - Si le canal n'est pas libre, alors transmettre plus tard.
    - Au cours de la transmission, écouter le canal.
    - S'il y a une collision, alors on arrête tout de suite la transmission pour retransmettre plus tard.
- Exemple de CSMA/CD:
    ![](/images/ch4/Screenshot_20231106_191334.png)
- Formules:
    - Tx >= 2 * Tp
    - L: Taille de la trame
    - Tx = L / Tp

### Normes IEEE 802 des LAN
- Plusieurs normes pour la couche MAC:
    - 802.3 (CSMA/CD)
    - 802.4 (TOKEN BUS)
    - 802.5 (TOKEN RING)
    - 802.6 (DQDB)
    - 802.9 (Integration Voice/Data)

#### Norme IEEE 802.3
##### Ethernet
- Transmission en bande de base, codage Manchester;
- Topologie en bus;
- Méthode d'accès selon la norme IEEE 802.3;
- Longeur de trames compromises entre minimum **64 octets** et maximum **1518 octets**;
- Support de type coaxial, paire torsadée et fibre optique;
- Basé sur CSMA/CD: écouter le canal tant qu'il est occupé, envoyer s'il est libre, arrêter la transmission et revenir plus tard si collision.
![](/images/ch4/Screenshot_20231106_194832.png)
>- 10 -> Vitesse de transmission;
>- Base -> Bande de base;
>- 2 -> spécificité du cable / longueur d'un segment.

##### Ethernet classique
![](/images/ch4/Screenshot_20231106_194515.png)

##### Format d'une trame
![](/images/ch4/Screenshot_20231106_195756.png)
- Préambule: 7 fois la suite 10101010 pour synchroniser l'horloge de l'émetteur avec celle du récepteur
- Start of frame delemiter: Pour dire que les informations utiles vont commencer
- Address: Généralement 48 bits
    - 3 premiers octets (00:00:00) = Manufacturier
        - 00:00:0C = CISCO
        - 08:00:5A = IBM
    -SI:
        - 1er bit (de gauche) de l'adresse destination = 0 -> adresse d'une seule machine (individuel)
        - 1er bit (de gauche) de l'adresse destination = 1 -> adresse d'un groupe de machines (Groupe)
        - Tous les bits de l'adresse destination = 1 -> diffusion
        - 2e bit (de gauche) de l'adresse de destination pour dire s'il s'agit d'une adresse locale (attribuée par le gestionnaire du réseau) ou une adresse globale/unique (attribuée par IEEE -> unique au monde)
- Données: minimum de 0 octets à 1500 octets
- Length: Nombre d'octets dans le champ de données
- Pad: des bits de remplissage pour avoir une longueur de la trame toujours > 64 octets
    - 64 = [46 du champ pad + 18 (minimum du total des autres champs)]
    - Cela permet d'éviter le cas qu'une station envoie une trame courte et quitte sans savoir s'il y a eu ou non une collision
        ![](/images/ch4/Screenshot_20231106_201115.png)
    - Checksum: Totale de contrôle. Détection d'erreurs basée sur un CRC

### Les ponts
- Inter-Networking
    - a) Couches implantées dans les équipements d'interconnexion
    - b) Structure d'une trame
![](/images/ch4/Screenshot_20231106_203640.png)
- Définition: Un équipement permettant d'interconnecter plusieurs réseaux LAN.
- Il intervient au niveau de la couche liaison, alors il n'analyse pas les paquets:
- Pourquoi?
    - Connecter plusieurs LAN différents (802.3, 802.4, 802.5, etc.) de différents départements d’une entreprise ou d’une organisation.
    - Si une entreprise est géographiquement répartie sur plusieurs bâtiments séparés et distants, alors il peut être plus économique d’avoir des LAN distincts interconnectés.
    - Diviser un LAN en plusieurs sous-LAN afin de diminuer la charge.
    - La distance entre les machines les plus éloignées dépasse la limite (2,5 km pour 802.3).
    - Fiabilité: Avoir plusieurs LAN à la place d’un seul augmente la fiabilité (un problème dans un LAN n’affectera pas toutes les stations).
    - Sécurité: Un pont peut vérifier la source et la destination, et refuser de diffuser une trame (agir selon une politique de sécurité).
-Fonctionnement: Il convertit principalement des trames d'un format à un autre.
    ![](/images/ch4/Screenshot_20231106_204138.png)
- Comparaison avec d'autres équipements d'interconnexion 
    ![](/images/ch4/Screenshot_20231106_204440.png)

# Section Pratique

## Protocoles

### Protocole Ethernet II
- Communication sur un réseau local (peer-to-peer)

![](/images/pratique/EN-ethernet-frame-structure6.jpg)

### Protocole IP
- Pour communiquer sur Internet

![](/images/pratique/IPFrame.png)

### Protocole ARP
- Pour trouver l'adresse MAC d'un hôte sur le réseau local
- Traduction d'adresse IP vers une adresse MAC

![](/images/pratique/ARPFrame.jpg)

- Afin d'êtr ecorrectement acheminée, une trame Ethernet II doit forcément avoir un couple IP-MAC correct dans les champs de destination

- Pour ne pas faire de requête ARP à chaque échange, chaque appareil garde une table ARP contenant le spaires d'adresses de leurs voisins. Cette table s'invalide automatiquement avec le temps.

- Vulnérabilité ARP
    - Man in the middle: attaque qui consiste à intercepter les communications entre deux machines afin de les espionner ou de les modifier à l'insu des deux parties.

> Le protocole RARP est l'inverse du protocole ARP. Il permet de trouver l'adresse IP d'un hôte sur le réseau local à partir de son adresse MAC.

### Protocole TTL: Time to live

- Détermine le nombre de routeurs qu'un paquet peut traverser avant d'être détruit.

- Permet d'éviter qu'un paquet circule sur le réseau indéfiniment.

- La RFC 1700 recommande une valeur de 64 pour le TTL.

- Les outils pour forger des paquets peuvent utiliser des TTL différents que l'OS.
    - Exemples:
        - Windows: 128
        - Linux: 64
        - MacOS: 255
        - Windows95: 32

- Le programme traceroute utilise le TTL pour déterminer le chemin qu'un paquet prend pour atteindre sa destination.
    - Envoi des paquets avec des TTL croissants
    - Lorsqu'un routeur décrémente le TTL à 0, il envoie un message ICMP 11 "Time Exceeded" à la source pour le lui signifier.
    - De cette façon, la source peut ainsi connaître le premier retour, puis le deuxieme, etc.

### Protocole ICMP
- Internet Control Message Protocol.
- Protocole de couche réseau
- Permet l'envoi de messages de contrôle et d'erreur.
- Permet de tester la connectivité IP.
- La commande ping utilise le protocole ICMP.
    - ping: Packet Internet Groper
        - Permet de savoir si une machine est accessible sur le réseau
        - Permet de mesurer le temps d'aller-retour d'un paquet à cette machine (RTT: Round Trip Time)

![](/images/pratique/ICMP-Header-Format.png)

### Protocole DNS

- Domain Name Service/System
- Associe un nom de domaine à une adresse IP
- Utile pour ne pas avoir à retenir les adresses IP des sites web.
- Idée: Associer une adresse IP malicieuse à un nom de domaine qui ne nous appartient pas.
    - Fonctionnement: Une faille du protocole DNS permet de faire croire à un routeur/serveur que l'adresse IP associée à un nom de domaine stock dans son cache a changé.

![Crédit: GeeksforGeeks](/images/pratique/dnsquerymessage.png)