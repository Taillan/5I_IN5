# Compte rendu TD1 Réseau avancé



## Mise en place d'un réseau local commute

###### 1 Combien de domaines de collision existent et combien existe-t-il de domaines de diffusions ?

Il y a 2 domaines de diffusions et 4 domaines de collisions et un domaine de diffusion

[Source](https://reussirsonccna.fr/domaine-de-collision-et-de-diffusion/)

#### Vérification de la configuration par défaut du commutateur : commande show

###### 2 Combien d’interfaces Fast Ethernet et de Gigabit Ethernet possède le switch ? A quoi servent-elles ?

24 Fast Ethernet et 2 Gigabit. Elles servent a communiquer sur le réseau

```bash
Switch#show startup-config 
startup-config is not present
```

Le switch répond cette réponse car il n'a reçu aucune configuration dans sa mémoire non-volatile pour le moment

###### 4 Quelles sont les caractéristiques de l’interface virtuelle VLAN1 : adresse IP, adresse MAC, activité, propriétés IP ?

```bash
Switch#show interfaces Vlan 1
Vlan1 is administratively down, line protocol is down
  Hardware is CPU Interface, address is 0040.0b22.dcc5 (bia 0040.0b22.dcc5)
  MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 21:40:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     1682 packets input, 530955 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicast)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     563859 packets output, 0 bytes, 0 underruns
     0 output errors, 23 interface resets
     0 output buffer failures, 0 output buffers swapped out
```

@IP : null
@MAC : **0040.0b22.dcc5**
Activité: **down**
Propriété: null
Queueing strategy: First in First out

###### 5 Quelles sont les propriétés par défaut de l’interface Fast Ethernet utilisée pour connecter votre PC. Adresse MAC, activité, vitesse, mode de transmission ? Quel événement pourrait activer une interface ?

```bash
Switch#show interfaces FastEthernet 0/1
FastEthernet0/1 is down, line protocol is down (disabled)
  Hardware is Lance, address is 000c.85d4.5001 (bia 000c.85d4.5001)
 BW 100000 Kbit, DLY 1000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Half-duplex, 100Mb/s
  input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     956 packets input, 193351 bytes, 0 no buffer
     Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 0 multicast, 0 pause input
     0 input packets with dribble condition detected
     2357 packets output, 263570 bytes, 0 underruns
     0 output errors, 0 collisions, 10 interface resets
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out
```

@MAC: 000c.85d4.5001
activité: down
vitesse: 100Mb/s
mode de transmission: Half-duplex

Quel événement pourrait activer une interface ?
La connexion d'un appareil active une interface réseau



###### 6 Quelles sont les paramètres VLAN par défaut du commutateur : nom du VLAN 1, ports attribués à ce VLAN, type du VLAN par défaut ?



```bash
Switch#show vlan 

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
```

nom: default

Port attribué:  Fa0/1, Fa0/2, Fa0/3, Fa0/4, Fa0/5, Fa0/6, Fa0/7, Fa0/8,Fa0/9, Fa0/10, Fa0/11, Fa0/12,Fa0/13, Fa0/14, Fa0/15, Fa0/16,Fa0/17, Fa0/18, Fa0/19, Fa0/20,Fa0/21, Fa0/22, Fa0/23, Fa0/24, Gig0/1, Gig0/2

Type: enet

##### CONFIGURATION DE BASE DU COMMUTATEUR

###### 7 Configurer un nouveau VLAN, par exemple VLAN 99. Attribuer une adresse IP et un masque de sous-réseau à l’interface VLAN 99 (192.168.10.99\24). Affectez le port connectant votre machine au VLAN 99. Utiliser la commande show pour vérifier votre configuration.

```bash
Switch#configure
Configuring from terminal, memory, or network [terminal]? 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 99
Switch(config-vlan)#exit
Switch(config)#int vlan 99
Switch(config-if)#ip address 192.168.10.99 255.255.255.0
Switch(config-if)#switchport mode access
Switch(config-if)#exit
Switch(config)#int f 0/1
Switch(config-if)#switchport access vlan 99
Switch(config-if)#end
```

Configuration effectué



```bash
Switch#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/1
                                                Gig0/2
99   VLAN0099                         active    Fa0/1
```

##### 

###### 8 Quelle est la bande passante définie sur cette interface VLAN99 ? Quelle est la stratégie de file d’attente ?

```bash
Switch#show int v99
Vlan99 is up, line protocol is down
  Hardware is CPU Interface, address is 0040.0b22.dc01 (bia 0040.0b22.dc01)
  Internet address is 192.168.10.99/24
  MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 21:40:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     1682 packets input, 530955 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicast)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     563859 packets output, 0 bytes, 0 underruns
     0 output errors, 23 interface resets
     0 output buffer failures, 0 output buffers swapped out

```

BW: BW 100000 Kbit
Queueing strategy: fifo ( first in first out )



