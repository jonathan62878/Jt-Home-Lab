# Jt-Home-Lab
Documentation of my windows, linux , networking. VMware, IT troubleshooting home labs


## Dual-Router Network Isolation Lab — August 17, 2026

### Objective

Build two separate physical networks, connect each network to VMware through a dedicated USB Ethernet adapter, and verify that the networks remain isolated.

### Network Configuration

| Device | Network | IP Address | Gateway | VMware Network |
|---|---|---|---|---|
| Windows 11 VM | Router 1 | 192.168.10.187/24 | 192.168.10.1 | VMnet2 |
| Ubuntu VM | Router 2 | 192.168.20.186/24 | 192.168.20.1 | VMnet3 |

### Physical Adapter Assignments

- LAB-RTR1-10 → Router 1 → 192.168.10.0/24
- LAB-RTR2-20 → Router 2 → 192.168.20.0/24
- VMnet2 bridged to LAB-RTR1-10
- VMnet3 bridged to LAB-RTR2-20

### Test Results

- Windows 11 successfully pinged Router 1 at 192.168.10.1.
- Ubuntu successfully pinged Router 2 at 192.168.20.1.
- Windows could not ping Ubuntu at 192.168.20.186.
- Ubuntu could not ping Windows at 192.168.10.187.
- Cross-network tests returned 100% packet loss.

### Conclusion

Both virtual machines received DHCP addresses from their assigned physical routers. Each VM could communicate with its local gateway, but traffic between the two subnets was blocked. This confirmed that the 192.168.10.0/24 and 192.168.20.0/24 networks were operating correctly and remained isolated.
