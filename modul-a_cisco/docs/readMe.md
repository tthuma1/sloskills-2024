
### Table 1: Seznam L2/L3 VLAN

| Ime VLAN         | VLAN ID | IP segment      |
|------------------|---------|-----------------|
| Uporabniki       | 110     | 10.1.10.0/24    |
| Gosti            | 120     | 10.1.20.0/24    |
| MGMT             | 130     | 10.1.30.0/24    |
| Alarm            | 140     | 10.1.40.0/24    |
| Strežniki DC     | 150     | 10.1.250.0/24   |
| DEMO_OKOLJE      | 240     | 10.1.10.0/24    |
| Zaposleni_PE     | 250     | 10.1.10.0/24    |
| MPLS-01_CORE-01  | 101     | Tabela 6        |
| MPLS-01_CORE-02  | 102     | Tabela 6        |
| INET-01_CORE-01  | 201     | Tabela 6        |
| INET-01_CORE-02  | 202     | Tabela 6        |

### Table 2: Seznam naslovni prostor za vmesnike Loopback in Tunel

| Naslovni prostor | IP segment      |
|------------------|-----------------|
| Loopback vmesniki| 192.[2-4].1.0/24|
| Tunelski vmesnik 1 | 192.1.2.0/24   |
| Tunelski vmesnik 2 | 192.1.3.0/24   |

### Table 3: Imena in IP-naslovi vmesnikov Loopback in Tunel

| Ime naprave     | Loopback 0       | Tunelski vmesnik |
|-----------------|------------------|------------------|
| R-INET-CB-01    | 192.2.1.1/32     | Tu1: 192.1.2.11  |
| R-MPLS-CB-01    | 192.2.1.10/32    | Tu2: 192.1.2.12  |
| SW-CORE-CB-01   | 192.2.1.2/32     | N/A              |
| SW-CORE-CB-02   | 192.2.1.3/32     | N/A              |
| SW-ACCESS-CB-01 | 192.2.1.5/32     | N/A              |
| SW-ACCESS-CB-02 | 192.2.1.6/32     | N/A              |
| R-DC-CB-01      | 192.2.1.12/32    | 192.1.2.13       |
| R-DC-CB-02      | 192.2.1.13/32    | 192.1.2.14       |
| R-BR-CB-01      | 192.4.1.100/32   | 192.1.2.15       |

### Table 4: Usmerjevalni protokoli in podatki o vrednosti ASN/AREA

| Ime naprave     | Usmerjevalni protokol | OSPF AREA   | ASN BGP | ASN WAN | ASN MPLS |
|-----------------|-----------------------|-------------|---------|---------|----------|
| R-INET-CB-01    | OSPF/EIGRP/BGP        | Area0       | 6450x   | 6500x   | N/A      |
| R-MPLS-CB-01    | OSPF/EIGRP            | Area0       | N/A     | 6500x   | 6450x    |
| SW-CORE-ZM-01   | OSPF                  | Area0       | N/A     | N/A     | N/A      |
| SW-CORE-ZM-02   | OSPF                  | Area0/Area1 | N/A     | N/A     | N/A      |
| R-DC-CB-01      | OSPF                  | Area1       | N/A     | N/A     | N/A      |
| R-DC-CB-02      | OSPF                  | Area1       | N/A     | N/A     | N/A      |
| R-BR-CB-01      | EIGRP                 | N/A         | N/A     | N/A     | 6500x    |

### Table 5: Seznam fizičnih povezav med napravami

| Ime naprave A   | Vmesnik naprave A | Vmesnik naprave B | Ime naprave B  |
|-----------------|-------------------|-------------------|----------------|
| R-INET-CB-01    | Fas 1             | Gig 1/0/2         | SW-CORE-CB-01  |
| R-INET-CB-01    | Fas 1             | Gig 1/0/3         | SW-CORE-CB-02  |
| R-MPLS-CB-01    | Fas 1             | Gig 1/0/21        | SW-CORE-CB-01  |
| R-MPLS-CB-01    | Fas 1             | Gig 1/0/23        | SW-CORE-CB-02  |
| SW-CORE-CB-01   | Gig 1/0/3         | Gig0              | R-DC-CB-01     |
| SW-CORE-CB-01   | Gig 1/0/4         | Gig0              | R-DC-CB-02     |
| SW-CORE-CB-01   | Gig 1/0/4         | Gig 1/0/4         | SW-ACCESS-CB-01|
| SW-CORE-CB-02   | Gig 1/0/21        | Gig 1/0/21        | SW-ACCESS-CB-01|
| SW-CORE-CB-02   | Gig 1/0/21        | Gig 1/0/22        | SW-ACCESS-CB-02|
| SW-ACCESS-CB-01 | Gig 1/0/22        | Fas 8             | R-BR-CB-01     |

### Table 6: IP-naslovi povezovalnih segmentov

| Ime naprave A  | IP naprave A     | IP naprave B     | Ime naprave B  |
|----------------|------------------|------------------|----------------|
| R-INET-CB-01   | 172.1.1.1/30     | 172.1.1.2/30     | SW-CORE-CB-01  |
| R-INET-CB-01   | 172.1.5.1/30     | 172.1.5.2/30     | SW-CORE-CB-02  |
| R-MPLS-CB-01   | 172.1.9.1/30     | 172.1.9.2/30     | SW-CORE-CB-01  |
| R-MPLS-CB-01   | 172.1.12.1/30    | 172.1.12.2/30    | SW-CORE-CB-02  |
| SW-CORE-CB-01  | 172.1.16.1/30    | 172.1.16.2/30    | R-DC-CB-01     |
| SW-CORE-CB-02  | 172.1.20.1/30    | 172.1.20.2/30    | R-DC-CB-02     |

### Table 7: MGMT IP-naslovi

| Ime naprave      | MGMT IP naslov     |
|------------------|--------------------|
| R-INET-CB-01     | N/A                |
| R-INET-MPLS-01   | N/A                |
| R-BR-ZM-01       | 10.30.1.2/24       |
| SW-CORE-CB-01    | 10.1.30.2/24       |
| SW-CORE-CB-02    | 10.1.30.3/24       |
| SW-ACCESS-CB-01  | 10.1.30.31/24      |
| SW-ACCESS-CB-02  | 10.1.30.32/24      |

### Tabela 8: Javni IP naslovni prostor

| Ekipa  | Omrežni segment ISP lokacija CL | Omrežni segment ISP lokacija PE |
|--------|--------------------------------|--------------------------------|
| Ekipa 1| 198.51.100.0/29               | 198.51.100.8/30                |
| Ekipa 2| 198.51.100.8/29               | 198.51.100.132/30              |
| Ekipa 3| 198.51.100.16/29              | 198.51.100.136/30              |
| Ekipa 4| 198.51.100.24/29              | 198.51.100.140/30              |

### Tabela 9: MPLS IP naslovni prostor

| Ekipa  | Omrežni segment MPLS lokacija CL | Omrežni segment MPLS lokacija PE |
|--------|---------------------------------|---------------------------------|
| Ekipa 1| 172.17.100.0/29                 | 172.17.100.224/29               |
| Ekipa 2| 172.17.100.8/29                 | 172.17.100.232/29               |
| Ekipa 3| 172.17.100.16/29                | 172.17.100.240/29               |
| Ekipa 4| 172.17.100.24/29                | 172.17.100.248/29               |