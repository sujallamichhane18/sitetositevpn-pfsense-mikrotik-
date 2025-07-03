# 🔐 Site-to-Site VPN: PfSense ↔ MikroTik

This project demonstrates a working Site-to-Site IPsec VPN tunnel between a **PfSense firewall** and a **MikroTik router**. It connects two LAN networks securely through an encrypted IPsec tunnel.

---
# Downloads
PfSense: https://www.pfsense.org/download/
MikroTik RouterOS: https://mikrotik.com/download

## 🧭 Network Overview

| Device     | WAN IP             | LAN Subnet         | LAN Gateway       |
|------------|--------------------|---------------------|--------------------|
| PfSense    | 192.168.110.155/24 | 192.168.20.0/24     | 192.168.20.1       |
| MikroTik   | 192.168.110.10/24  | 192.168.30.0/24     | 192.168.30.1       |
| PC1        | -                  | 192.168.20.10/24    | 192.168.20.1       |
| PC2        | -                  | 192.168.30.10/24    | 192.168.30.1       |

---

## 🎯 Objective

Establish a secure **IPsec VPN** tunnel between the two networks:

- From: `192.168.20.0/24` (Site A)
- To: `192.168.30.0/24` (Site B)

---

## 🖼️ Topology Diagram

You can find the network diagram in the `sitetositevpn.png` 


---

## ⚙️ Basic Configuration

### 🔸 PfSense IPsec

**Phase 1:**
- Remote Gateway: `192.168.110.10`
- Authentication: Pre-Shared Key
- IKE Version: IKEv1
- Encryption: AES-256, SHA256, DH Group 14
- Lifetime: 28800

**Phase 2:**
- Local Network: `192.168.20.0/24`
- Remote Network: `192.168.30.0/24`
- Protocol: ESP
- Encryption: AES-256, SHA256, PFS Group 14
- Lifetime: 3600

**Firewall Rules:**
- Allow UDP 500 & 4500 on WAN
- Allow ESP on WAN
- Allow all traffic on IPsec interface

---

### 🔹 MikroTik IPsec

```
/ip ipsec proposal
add name=pfsense-proposal auth-algorithms=sha256 enc-algorithms=aes-256-cbc pfs-group=modp2048

/ip ipsec peer
add address=192.168.110.155/32 exchange-mode=main secret=YourSecretKey \
    local-address=192.168.110.10 profile=default

/ip ipsec policy
add src-address=192.168.30.0/24 dst-address=192.168.20.0/24 sa-dst-address=192.168.110.155 \
    sa-src-address=192.168.110.10 tunnel=yes proposal=pfsense-proposal

/ip firewall nat
add chain=srcnat src-address=192.168.30.0/24 dst-address=192.168.20.0/24 action=accept

/ip firewall filter
add chain=input protocol=udp port=500,4500 action=accept
add chain=input protocol=ipsec-esp action=accept
```
✅ Verification
Ping from PC1 → PC2

Ping from PC2 → PC1

On PfSense: Status > IPsec

On MikroTik:
```
Copy
Edit
/ip ipsec installed-sa print
```
