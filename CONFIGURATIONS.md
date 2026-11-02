# Configurations – VLAN et trunk 802.1Q (partie C)

Configuration complète de chaque équipement, exportée depuis le fichier Packet Tracer.
Les mots de passe et numéros de série sont masqués ; les interfaces sans configuration sont omises.
Les fichiers bruts (un par équipement) sont dans [`configs/`](configs/).

## Sommaire

- [Switch0](#switch0) – Switch 2960-24TT
- [Switch1](#switch1) – Switch 2960-24TT
- [Postes et serveurs](#postes-et-serveurs)

## Postes et serveurs

| Nom | Type | Adresse IP | Masque | Passerelle | DNS |
|---|---|---|---|---|---|
| PC0 | Pc | 192.168.10.10 | 255.255.255.0 | – | – |
| PC1 | Pc | 192.168.10.11 | 255.255.255.0 | – | – |
| PC2 | Pc | 192.168.20.10 | 255.255.255.0 | – | – |
| PC3 | Pc | 192.168.10.12 | 255.255.255.0 | – | – |
| PC4 | Pc | 192.168.20.11 | 255.255.255.0 | – | – |
| PC5 | Pc | 192.168.20.12 | 255.255.255.0 | – | – |

## Switch0

Switch · modèle 2960-24TT · hostname `Switch`

```cisco
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/2
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/3
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/24
 switchport trunk allowed vlan 10,20
 switchport mode trunk
!
interface Vlan1
 no ip address
 shutdown
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
end
```

## Switch1

Switch · modèle 2960-24TT · hostname `Switch`

```cisco
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
!
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/3
 switchport access vlan 20
 switchport mode access
!
interface FastEthernet0/24
 switchport trunk allowed vlan 10,20
 switchport mode trunk
!
interface Vlan1
 no ip address
 shutdown
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
end
```
