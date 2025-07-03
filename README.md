# Site-to-Site VPN: PfSense to MikroTik

This project demonstrates a simple IPsec Site-to-Site VPN setup between a PfSense firewall and a MikroTik router.

## 🧭 Network Overview

- **PfSense LAN**: 192.168.20.0/24  
- **MikroTik LAN**: 192.168.30.0/24  
- **WAN Segment**: 192.168.110.0/24  
- **VPN Type**: IPsec (IKEv1)

## 📌 Objective

Allow devices in each LAN (PC1 and PC2) to communicate securely over an IPsec tunnel.

## 🖼️ Topology Diagram

See `sitetositevpn.png` for a visual reference.

## ✅ Status

- [x] VPN tunnel established  
- [x] LAN-to-LAN communication tested  
- [x] No NAT interference  
