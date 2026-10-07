# Enterprise Network Topology & Cisco Configuration Simulation

Bu layihədə Cisco Packet Tracer mühitində 3 səviyyəli (Hierarchical Campus Network Model) Korporativ Şəbəkə İnfrastrukturu sıfırdan layihələndirilmiş, fiziki kabellənmiş və bütün Layer 2 / Layer 3 konfiqurasiyaları tətbiq olunmuşdur.

## 📐 Şəbəkə Topologiyası

![Network Topology](topology.png)

## 🚀 İstifadə Olunan Cihazlar və Modellər

- **1x ISP Router:** `Cisco 2911` (İnternet Provayder Simulyasiyası)
- **1x Enterprise Edge Router:** `Cisco 2911` (`HQ-ROUTER` - NAT, OSPF, Dynamic Routing)
- **2x Core / Distribution Switch:** `Cisco 3560-24PS` (`HQ-CORE-SW1` & `HQ-CORE-SW2` - L3 Switching, HSRP, EtherChannel, Inter-VLAN Routing)
- **1x Access Switch:** `Cisco 2960-24TT` (`HQ-ACCESS-SW1` - VLAN-lar, Port Security, DHCP Snooping)
- **1x DHCP Server:** `DHCP-Radius-Server` (VLAN 10 - Mərkəzi İP Paylanması)
- **1x DNS Server:** `Google-DNS-Server` (`8.8.8.8` - İnternet çıxış testi üçün)
- **İstifadəçi Qurğuları:** Müxtəlif VLAN-larda yerləşən işçi və qonaq kompyuterləri (PC)

## 🛠️ Tətbiq Olunan Texnologiyalar və Konfiqurasiyalar

### 1. Layer 2 (Switching & Redundancy)
- **VLAN Segmentation:** 
  - `VLAN 10`: SERVERS (`192.168.10.0/24`)
  - `VLAN 20`: ADMIN (`192.168.20.0/24`)
  - `VLAN 30`: USERS (`192.168.30.0/24`)
  - `VLAN 40`: GUESTS (`192.168.40.0/24`)
  - `VLAN 99`: NATIVE_UNUSED
- **802.1Q Trunking & DTP:** Switch-lər arası VLAN trafikinin ötürülməsi.
- **EtherChannel (LACP):** Core Switch-lər arasında ötürmə qabiliyyətini və ehtiyatlılığı artırmaq üçün FastEthernet 0/23-24 portlarının aggreqasiyası.
- **Spanning Tree Protocol (Rapid PVST+):** Şəbəkə dövrələrinin (Loop) qarşısının alınması.

### 2. Layer 3 (Routing & High Availability)
- **Inter-VLAN Routing:** Core Switch-lərdə SVI vasitəsilə VLAN-lar arası məntiqi əlaqə.
- **HSRP (First Hop Redundancy Protocol):** Core Switch-lər arasında Virtual Gateway (`192.168.x.1`) vasitəsilə fəlakətə dözümlülük (Active/Standby).
- **OSPF Dynamic Routing:** Core Switch-lər və Edge Router arasında avtomatik marşrutlaşdırma mübadiləsi.
- **DHCP Relay Agent (`ip helper-address`):** İP ünvan sorğularının mərkəzi serverə yönləndirilməsi.

### 3. Network Security & Internet Access
- **Port Security:** Access portlarında icazəsiz cihazların qoşulmasının önlənməsi (`sticky MAC`, `violation restrict`).
- **DHCP Snooping:** Saxta (Rogue) DHCP serverlərin şəbəkəyə müdaxiləsinin qarşısının alınması.
- **NAT / PAT (Port Address Translation):** Daxili İP ünvanların xarici qlobal İP-yə çevrilərək `8.8.8.8` (İnternet) çıxışının təmin edilməsi.

## ✅ Test və Nəticə

- **VLAN & Routing Test:** Bütün VLAN-larda yerləşən PC-lər Gateway və mərkəzi DHCP Server ilə maneəsiz əlaqə qurur.
- **Failover Test:** Əsas Core Switch sıradan çıxdıqda HSRP sayəsində trafik avtomatik olaraq ehtiyat Core Switch-ə keçir.
- **NAT & Internet Test:** `PC-user1` üzərindən `ping 8.8.8.8` əmri ilə paketlərin xarici şəbəkəyə uğurla çatdığı təsdiqlənmişdir.

## 📁 Layihə Faylı
İnfrastrukturun `.pkt` faylını yükləyərək **Cisco Packet Tracer** proqramında açıb canlı simulyasiya və konfiqurasiyaları nəzərdən keçirə bilərsiniz.
