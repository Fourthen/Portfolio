# Android TV — Home Network Security Audit
Tools: Kali Linux, nmap, ADB, iptables, VirtualBox

---

## Target Device

| Property | Value |
|----------|-------|
| Model | (Google TV) |
| Chipset | Realtek RTK5 |
| Kernel | Linux 5.4.242 |
| Security Patch | 2025-07-01 |
| SELinux | Enforcing |

---

## Setup & Network Isolation

Kali VM deployed in VirtualBox with bridged networking. 

---

## Network Discovery


nmap -sn xxxx

## Open Ports on TV

nmap -sV xxxx


| Port | Service | Risk |
|------|---------|------|
| 5555 | ADB (Android Debug Bridge) | **HIGH** — full device control |
| 8008 | HTTP (Chromecast discovery) | MEDIUM |
| 8009 | CastV2 (Chromecast control) | MEDIUM |
| 8443 | HTTPS management | LOW |
| 9000 | Smart TV service listener | LOW |

---

## ADB Access

Enabled Developer Options (Build number × 7) and USB debugging on the TV. ADB port 5555 opened on the network, allowing remote shell access from Kali.

```bash
adb connect xxxx:5555
adb shell getprop ro.product.model       
adb shell getprop ro.build.display.id   
adb shell getenforce                     
```

With ADB access an attacker on the same LAN could: take screenshots, sideload malware, grant dangerous permissions silently, exfiltrate files, use the TV as a network pivot point, or brick the device.

---

## Permission Audit

Multiple system apps have **RECORD_AUDIO: granted=true** with `SYSTEM_FIXED | GRANTED_BY_DEFAULT` flags — meaning the user was never asked, and the permission **cannot be revoked** without root.

Microphone: 6 audio capture devices found under `/dev/snd/`. Mic is unmuted.

Camera: `CAMERA: granted=true` on several system apps despite the device having **0 cameras**. However, the Camera HAL is configured for external USB — plugging in a USB webcam would give pre-authorized apps instant access.

```bash
adb shell dumpsys media.camera
# Number of camera devices: 0
# Camera Provider HAL external/0 — ready for USB camera

adb shell ls /dev/snd/ | grep c$
# pcmC0D0c through pcmC0D4c + pcmC1D0c — 6 capture devices

adb shell dumpsys audio | grep -i "mic"
# mic mute FromSwitch=false FromRestrictions=false FromApi=false
```

---

## Outbound Connections (Idle)

With the TV sitting on the home screen doing nothing, `netstat` revealed **20+ active connections**:

| Purpose | 
|-------------|
| Google services & APIs |
| Firebase Cloud Messaging (push notifications) |
| Google (likely ads/analytics) |
| Amazon AWS (S3) |
|  Google Cloud |
| Unknown Finnish IP |
| Google DNS (bypassing router DNS) |

---

## Root Feasibility

| Vector | Result |
|--------|--------|
| Dirty Pipe (CVE-2022-0847) | N/A — requires kernel ≥5.8 |
| Dirty COW (CVE-2016-5195) | Patched |
| SELinux | Enforcing — blocks escalation |
| Bootloader unlock | No public method for Thomson/Realtek |
| su binary | Not found on device |

Verdict: Root not feasible without hardware-level attack (UART/serial).

---

## Findings Summary

| Finding | Risk | Mitigation |
|---------|------|------------|
| ADB accessible on LAN when enabled | HIGH | Disable Developer Options after testing |
| Irrevocable mic permissions (SYSTEM_FIXED) | HIGH | Cannot revoke without root |
| Pre-granted camera perms (no hardware) | MEDIUM | Don't connect USB cameras to TV |
| 20+ idle outbound connections | MEDIUM | Deploy Pi-hole / DNS filtering |
| Chromecast ports open on LAN | MEDIUM | VLAN segmentation for IoT |
| SELinux enforcing | GOOD | No action needed |
| Security patch up to date | GOOD | Keep firmware updated |

---

## Key Takeaways

1. ADB is the biggest risk — anyone on your LAN can get full control of the TV when it's enabled
2. Smart TVs are surveillance-ready by default — irrevocable mic access, constant telemetry, pre-granted permissions the user never approved
3. Network segmentation matters — IoT devices like smart TVs should be on their own VLAN, isolated from sensitive devices
4. Consumer devices prioritize features over privacy — 20+ connections while idle, DNS bypassing local resolver, phoning home to ad networks
