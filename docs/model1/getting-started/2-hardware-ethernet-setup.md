---
layout: default
title: Hardware Ethernet Setup
authors:
    - Elias Dandouch
    - Scott Feister
---
# Step 1: Hardware / Ethernet Setup (10 minutes)

### Physical Connection Setup
Before flashing your SD cards, let's establish the physical network infrastructure:

1. **Router Connection**: Ensure your router/switch has at least 2 available Ethernet ports
2. **Cable Preparation**: Have both Ethernet cables ready - you'll connect these after the Pi devices boot
3. **Power Supply Check**: Verify both Pi power supplies are functional
4. **Network Planning**: Note your router's IP range (typically 192.168.1.x or 192.168.0.x)

### Router Access Verification
1. Access your [router's administrative panel](https://www.lifewire.com/accessing-your-router-at-home-818205)
2. Navigate to the "Connected Devices" or "DHCP Clients" section
3. Familiarize yourself with the interface - you'll use this to find your Pi devices later

**Why Ethernet First?**: Ethernet provides the most reliable initial connection. Once SSH is established, you can configure WiFi as needed.

### macOS Network Priority Issue

**Problem**: If you're using macOS, your Mac will always prioritize direct Ethernet connections even when they don't provide internet access. This can be frustrating when you need internet access while SSH'd into your Pi devices.

**Solution**: Reorder your network service priorities to prioritize WiFi over Ethernet adapters.

**Step 1**: Check current network priority:
```bash
networksetup -listnetworkserviceorder
```

**Step 2**: Identify the problem - if you see Ethernet adapters (like AX88179A) listed before WiFi, this will cause the issue.

**Step 3**: Reorder services to prioritize WiFi:
```bash
sudo networksetup -ordernetworkservices "Wi-Fi" "AX88179A" "TI_AM335x_BeagleBone_Black" "Thunderbolt Bridge" "iPhone USB"
```
*Note: Adjust the service names to match your specific output from Step 1.*

**Step 4**: Verify the change:
```bash
networksetup -listnetworkserviceorder
```

WiFi should now appear as priority (1) in the list. You can now connect Ethernet cables to your Pi devices without losing internet access on your Mac.

---
