Glede na tabelo 5 ustrezno fizicno povezemo naprave a)

# Agregacija povezav b)
```
    #Raba LACP agregacije (PortChannel)
    #Konf.: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/15-2_2_e/configuration/guide/b_1522e_2960_2960c_2960s_2960sf_2960p_cg/m_1522e_layer2_etherchanl_2960_2960s_cg.html

    interface range Ethernet11/2 - 3 #SW-CORE-CB-01 <--> SW-CORE-CB-02
    interface range Ethernet0/0 - 1 #SW-ACCESS-CB-01 <--> SW-ACCESS-CB-02
    channel-group 10 mode active
    channel-protocol lacp
    exit
    interface port-channel 10
    #preveri stanje enkapsulacije trunk vmensikov (ce je na obeh straneh auto ne bo delal, moras spremeniti na dot1q, enako velja potem za port-channel)
    switchport mode trunk
    #switchport trunk allow vlan <-vlans,...->
    lacp rate fast

    #Pri nastavitvi VLAN-ov, jih mjoramo nastaviti na nivoju ether-channel
```

# Nastavitev VTP c)
```
    VTP: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/15-2_2_e/configuration/guide/b_1522e_2960_2960c_2960s_2960sf_2960p_cg/m_1522e_vlan_vtp_2960s_cg.html

    vtp domain cbank
    vtp version 3
    vtp password cbank@123 hidden
    
    vtp mode server vlan #Za W-CORE-CB-01 (VTP server)
    vtp mode server mst 
    vtp primary mst #SPodnja ukaza izvrsimo v exec mode
    vtp primary vlan

    vtp mode client vtp#Za ostala stikala
    vtp mode client mst

    #Za razhroscevanje
    #show vtp status
```

# Nastavitve VLAN d) in e)
```
    #Nastavljamo na W-CORE-CB-01 (VTP server)

    vlan <-vlan id->
    name <-vlan ime->

    #Pri nastavljanju VLAN-ov na PortChannel vmesnikih moramo paziti, da so nastavitve
    #enake na vseh, ki pripadajo enakem PortChannel vmensiku, drugace nastavitve ne
    #bodo delovale!

    interface range Ethernetx - y
    switchport mode trunk
    switchport trunk allow vlan 110,120,130,140,150,240,250,101,102,201,202
    switchport trunk native vlan 505
    #switchport trunk allow vlan 130 100

    #Razhroscevanje VLAN-ov
    #show vlan brief
    #show interfaces trunk|...
```

# Nastavitev MST f)
Ni se dokoncano!!
```
    #MST: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/15-2_2_e/configuration/guide/b_1522e_2960_2960c_2960s_2960sf_2960p_cg/m_1522e_layer2_mstp_2960_2960s_cg.html
    #
    #https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/24248-147.html

    spanning-tree mode mst

    spanning-tree mst configuration #Za W-CORE-CB-01 (VTP server)
    name cbank
    instance 1 vlan 1, 110, 120
    instance 2 vlan 130, 140
    spanning-tree mst 1 root primary

    spanning-tree mst 2 root primary #Za SW-CORE-CB-02

    spanning-tree mst configuration #Za ostala stikala

    #Razhroscevnje MST nastavitev
    #show spanning-tree mst configuration
    #show mst summary
    #show spanning-tree vlan <-vlan id->
```

# Povezljivost VLAN-ov g)
Ni se dokoncano!!
```
    interface ethernetx.<-vlan id->
    encapsulation dot1q <-vlan id->
    ip address <-ip-> <-maska->

    ip routing    
```
