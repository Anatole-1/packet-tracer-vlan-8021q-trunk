# VLAN répartis sur deux switchs avec trunk 802.1Q – Contrôle réseaux (partie C)

Contrôle de réseaux réalisé à l'ESAIP (IR3), partie C : deux VLAN (Étudiants / Enseignants) répartis sur deux switchs Cisco 2960, reliés par un lien trunk 802.1Q qui ne laisse passer que les VLAN autorisés.

![Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer%208.2-1BA0D7?logo=cisco&logoColor=white)
![Switching](https://img.shields.io/badge/Switching-VLAN%20%2F%20802.1Q-informational)

## Topologie

### Capture Packet Tracer

![Topologie sous Packet Tracer](images/topologie.jpg)

### Schéma logique

```mermaid
graph LR
  subgraph A[" "]
    PC0["PC0 – VLAN 10<br/>192.168.10.10"] ---|Fa0/1| SW0[Switch0]
    PC1["PC1 – VLAN 10<br/>192.168.10.11"] ---|Fa0/2| SW0
    PC2["PC2 – VLAN 20<br/>192.168.20.10"] ---|Fa0/3| SW0
  end
  SW0 ===|"Fa0/24 ↔ Fa0/24<br/>Trunk 802.1Q (VLAN 10,20)"| SW1[Switch1]
  subgraph B[" "]
    SW1 ---|Fa0/1| PC3["PC3 – VLAN 10<br/>192.168.10.12"]
    SW1 ---|Fa0/2| PC4["PC4 – VLAN 20<br/>192.168.20.11"]
    SW1 ---|Fa0/3| PC5["PC5 – VLAN 20<br/>192.168.20.12"]
  end
```

## VLAN et adressage

| VLAN | Nom | Réseau | Postes |
|---|---|---|---|
| 10 | Etudiants | 192.168.10.0 /24 | PC0, PC1 (Switch0) · PC3 (Switch1) |
| 20 | Enseignants | 192.168.20.0 /24 | PC2 (Switch0) · PC4, PC5 (Switch1) |

## Configuration type

```cisco
vlan 10
 name Etudiants
vlan 20
 name Enseignants
!
interface FastEthernet0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

Toutes les configurations sont regroupées dans [`CONFIGURATIONS.md`](CONFIGURATIONS.md).

## Compétences mises en œuvre

- VLAN étendus sur plusieurs switchs
- Trunk 802.1Q et filtrage des VLAN autorisés (`allowed vlan`)
- Vérification : `show interfaces trunk`, `show vlan brief`, `ping` entre postes d'un même VLAN sur des switchs différents

## Utilisation

Ouvrir [`controle-vlan-partie-c.pkt`](controle-vlan-partie-c.pkt) avec **Cisco Packet Tracer 8.2** ou plus récent.

## Voir aussi

- [Partie A – Segmentation VLAN sur un seul switch](https://github.com/Anatole-1/packet-tracer-vlan-single-switch)

## Contenu du dossier

| Élément | Description |
|---|---|
| [`controle-vlan-partie-c.pkt`](controle-vlan-partie-c.pkt) | Fichier Cisco Packet Tracer du projet |
| [`CONFIGURATIONS.md`](CONFIGURATIONS.md) | Configuration de chaque équipement et adressage des postes, en un seul fichier |
| [`configs/`](configs/) | Une configuration brute par équipement (`.txt`) |
| [`images/`](images/) | Captures de la topologie |

## Auteur

**Anatole BERNARD** – étudiant ingénieur à l'ESAIP
