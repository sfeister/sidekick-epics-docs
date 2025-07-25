---
layout: default
title: WiFi Configuration (Optional)
authors:
    - Elias Dandouch
    - Scott Feister
---
# Step 2: WiFi Configuration (Optional - 5 minutes)

While Ethernet is recommended for initial setup, you can configure WiFi during the OS imaging process:

### During OS Imaging (Recommended)
- Configure WiFi credentials in the Raspberry Pi Imager's "Advanced Options"
- This allows WiFi as a backup if Ethernet fails
- Useful for portable setups or locations without available Ethernet ports

### After Initial Setup (Alternative)
- Connect via Ethernet first, then configure WiFi through SSH
- Edit `/etc/wpa_supplicant/wpa_supplicant.conf` manually
- More complex but provides flexibility for network changes

**Note**: For this tutorial, we'll primarily use Ethernet for reliability, with WiFi as optional backup.

---