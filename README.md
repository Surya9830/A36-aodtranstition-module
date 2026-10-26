Floating Feature HighEnd --- Samsung AOD Clock Transition
A KernelSU systemless module that modifies selected Samsung
floating_feature.xml values. It was tested by the maintainer on a
Samsung Galaxy A36 5G (a36xq).
Status: AOD clock-transition tweak reported working on the
maintainer's device. Other devices and firmware versions have not been
verified.

Features
- Sets SEC_FLOATING_FEATURE_LAUNCHER_CONFIG_ANIMATION_TYPE to
  HighEnd.
- Adds clocktransition and activeclock=4 to
  SEC_FLOATING_FEATURE_FRAMEWORK_CONFIG_AOD_ITEM.
- Uses a KernelSU module overlay rather than directly modifying the
  read-only system/vendor partitions.
Compatibility
- Tested device: Samsung Galaxy A36 5G (a36xq)
- Root/module manager: KernelSU with a compatible overlay/mounting
  setup
- Firmware: The exact firmware/build may affect results; not all
  One UI versions have been tested.
- Other devices: Unknown. Do not assume compatibility.
The flags are firmware-dependent. Enabling them does not guarantee that
every device supports the corresponding animation or UI behavior.
Installation
1. Make a backup of your important data and keep a copy of your current
   working module/ZIP.
2. Download the flashable ZIP from the repository's Releases
   section (or the ZIP attached to the relevant release).
3. Open KernelSU Manager.
4. Disable or remove an older version of this module first, to avoid
   overlapping overlays.
5. Install the ZIP using KernelSU's module installation flow.
6. Reboot the phone.
7. Test the AOD clock transition by locking the screen and observing
   the transition to Always On Display.
If the phone behaves unexpectedly, disable or remove the module in
KernelSU and reboot. Keep a backup of the original module and know how
to access KernelSU recovery/disable procedures before experimenting.
What it changes
The module provides XML overlays at these paths:
system/etc/floating_feature.xml
vendor/etc/floating_feature.xml
Relevant values:
<SEC_FLOATING_FEATURE_FRAMEWORK_CONFIG_AOD_ITEM>aodversion=7,clocktransition,activeclock=4</SEC_FLOATING_FEATURE_FRAMEWORK_CONFIG_AOD_ITEM>
<SEC_FLOATING_FEATURE_LAUNCHER_CONFIG_ANIMATION_TYPE>HighEnd</SEC_FLOATING_FEATURE_LAUNCHER_CONFIG_ANIMATION_TYPE>
The module uses the complete XML files with the relevant values changed;
it should not replace a full feature XML with a file containing only
these two lines.
Verification
After rebooting, you can inspect the active values from a computer with
ADB and root access:
adb shell su -c "grep 'SEC_FLOATING_FEATURE_FRAMEWORK_CONFIG_AOD_ITEM' /system/etc/floating_feature.xml"
adb shell su -c "grep 'SEC_FLOATING_FEATURE_LAUNCHER_CONFIG_ANIMATION_TYPE' /vendor/etc/floating_feature.xml"
Expected values include clocktransition,activeclock=4 for the AOD
entry and HighEnd for the launcher animation entry.

These commands verify the visible XML values; they do not by themselves
prove that every feature is supported by the firmware.
Troubleshooting
- No visible change: Confirm the module is enabled, reboot, and
  check the active XML values. Firmware may ignore unsupported flags.
- Boot or UI problems: Disable/remove the module from KernelSU and
  reboot.
- Another module edits the same XML: Disable overlapping modules
  while testing so you can identify which overlay is active.
Disclaimer
This is an unofficial, community-made modification. Use it at your own
risk. It may cause unexpected UI behavior or instability, and behavior
may change after firmware updates. Always keep a backup and a recovery
plan. The maintainer does not guarantee compatibility or provide a
warranty.

Samsung and Galaxy are trademarks of Samsung Electronics. This project
is not affiliated with or endorsed by Samsung.
