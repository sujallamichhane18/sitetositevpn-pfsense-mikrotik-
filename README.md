
---

```markdown
# 🔐 PfSense ↔ MikroTik Site-to-Site VPN

This project demonstrates a basic **Site-to-Site IPsec VPN** setup between a **PfSense firewall** and a **MikroTik router** to securely connect two different LANs.

## 🖥️ Network Topology

```

\[ PC1 ] ── 192.168.20.10
|
\[ PfSense Firewall ]
└── LAN: 192.168.20.1/24
└── WAN: 192.168.110.155/24
|
\|  IPsec VPN Tunnel
|
┌────WAN: 192.168.110.10/24
\[ MikroTik Router ]
└── LAN: 192.168.30.1/24
|
\[ PC2 ] ── 192.168.30.10

```

## 📋 Description

- The VPN tunnel securely connects:
  - **Site A (PfSense)**: `192.168.20.0/24`
  - **Site B (MikroTik)**: `192.168.30.0/24`
- Devices in each LAN can communicate with each other through the encrypted tunnel.
- Useful for branch-to-branch connections, secure remote access, or hybrid lab setups.

## 🧪 Tested Features

- Successful IPsec tunnel establishment
- Full bidirectional ping between PC1 and PC2
- No NAT interference (routing-based setup)

## 📁 Files

- `diagrams/`: Includes the network diagram image
- `README.md`: You're reading it!

## ✍️ Author

Created by **Sujal Lamichhane**

```

---
