# Govee

[![Add To Installation](https://marketplace.signalrgb.com/resources/add-extension-256.png 'Add to My SignalRGB Installation')](signalrgb://addon/install?url=https://github.com/omidchini/signalrgb_govee)

## Getting started
This is a SignalRGB Addon to add support for Govee Wi-Fi devices to SignalRGB, with several fixes and improvements over the original.

### Based on https://gitlab.com/signalrgb/Govee

---

## Changelog

### Cross-subnet / Manual IP Support
- Added a **Manually Specify IP Address** field in the discovery UI for setups where the SignalRGB PC and Govee device are on different subnets (e.g. main LAN vs IoT VLAN).
- The discovery service now performs unicast scans to manually specified IPs on startup and on every periodic poll, bypassing the multicast discovery limitation (`239.255.255.250` does not cross subnet boundaries without special router configuration).
- Added subnet hint text in the UI to guide users in cross-subnet setups.

### Bug Fixes
- Fixed subdevice RGB data collection — colors are now correctly pushed per-LED rather than indexed into a pre-sized array, resolving incorrect color mapping on multi-bar devices (e.g. H6046, H6056, H6168).
- Removed leftover `enabledBrightness` property and the associated `SetBrightness(enabledBrightness)` call on initialize, which referenced a removed controllable parameter.
- Fixed incorrect use of `service.log` vs `device.log` inside `UdpSocketServer` connection and error handlers.

---

## Known Issues
- Devices that do not support LAN Control do not work.
- Initial device scan may take several minutes on first run.
- Devices that do not support the Razer Chroma or DreamView protocol will only show as a single color zone.

## Cross-Subnet Setup (IoT VLAN)
If your Govee device is on a separate subnet or VLAN from your PC:

1. Ensure your router allows UDP traffic between the PC and Govee device on ports **4001**, **4002**, and **4003**.
2. If using masquerade/NAT for inter-VLAN traffic, make sure return UDP traffic can reach your PC.
3. In the SignalRGB plugin discovery UI, enter the **static IP address** of your Govee device in the **"Manually Specify IP Address"** field and press Enter.
4. The device will be discovered and cached for future startups.

> Note: Multicast-based auto-discovery (`239.255.255.250:4001`) will not work across subnets unless your router is configured with IGMP proxy or multicast routing.

## Installation
Click the button above and allow SignalRGB to install this extension when prompted.

## Support
Feel free to open issues here, or join the SignalRGB Testing Server and post an issue there https://discord.com/invite/J5dwtcNhqC.