```
    enable #en
    configure terminal #conf t
```

# Nastavljanje ime naprave a)
```
    hostname <-ime naprave->
```

# Nastavljanje Loopback vmesnikov b)
```
    #https://www.cisco.com/c/en/us/td/docs/security/asa/asa919/configuration/general/asa-919-general-config/interface-loopback.pdf
    
    interface loopback 0
    ip address <-ip naslov-> <-maska->
```

# Nastavljanje SSHv2 povezave in uporabnika c) in d)
```
    #https://ipwithease.com/how-to-configure-ssh-version-2-on-cisco-router/
    #aaa: https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus3600/sw/92x/security/configuration/guide/b-cisco-nexus-3600-nx-os-security-configuration-guide-92x/b-cisco-nexus-3600-nx-os-security-configuration-guide-92x_chapter_011.pdf

    #Uporabnik: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst_pon/software/configuration_guide/mng_usrs/b-gpon-config-managing-users/user_management.html

    aaa new-model
    aaa authentication login default local
    ip domain-name cbank.local
    username netadmin privilege 15 secret SuperGeslo@2024
    service password-encryption
    login local
    #username netadmin terminal all #Nevem ce je potrebno, ne dela

    ip ssh rsa keypair-name sshkey
    crypto key generate rsa usage-keys label sshkey modulus 1024
    ip ssh version 2

    line vty 0 4
    login authentication default
    transport input ssh

    #Razhroscevalni ukazi:
    #
    #show ssh
    #show ip ssh
    #debug ip ssh
```

# Nastavljanje dodatnega uporabnika e)
```
    #https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/sec_usr_aaa/configuration/xe-16-10/sec-usr-aaa-xe-16-10-book/sec-aaa-comm-criteria-pwd.html

    aaa common-criteria policy CB-URGENT
    min-length 10
    special-case 1
    upper-case 1
    lower-case 1
    lifetime month 6

    username urgent common-criteria-policy CB-URGENT secret SuperGeslo@2024
```

# Nastavljanje sistemskega casa f)
```
    #Moznost NTP: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/15-2_2_e/configuration/guide/b_1522e_2960_2960c_2960s_2960sf_2960p_cg/m_1522e_sm_swadmn_2960_2960s_2960c_cg.html#ID24

    clock timezone CET -1
    clock summer-time CEST recurring last Sun Mar 2:00 last Sun Oct 3:00
```

# Nastavljanje zajema dnevniskih zapisov in stevilo zapisov g) in i)
```
    #https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-12/configuration_guide/sys_mgmt/b_1612_sys_mgmt_3650_cg/configuring_system_message_logs.html

    logging buffered 200000
    service timestamps log datetime msec localtime year show-timezone
    service timestamps debug datetime msec localtime year show-timezone
```

# Nastavljanje sporocilo dneva h)
```
    banner motd $Vegovci so zakon!$
```

# Shranjenje konfiguracije
```
    # Shrani nastavitve
    copy running-config startup-config
```