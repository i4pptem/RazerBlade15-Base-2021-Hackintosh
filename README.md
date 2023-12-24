<img align="right" src="https://raw.githubusercontent.com/acidanthera/OpenCorePkg/master/Docs/Logos/OpenCore_with_text_Small.png" alt="OpenCore 0.7.0" width="225">

# Razer Blade 15 Base 2021 (RZ09-0369x) Hackintosh
macOS Sonoma on Razer Blade 15 Base (2021) RZ09-0369x on Acidanthera's OpenCore bootloader

This EFI folder is based on [Japerz12138's repository](https://github.com/Japerz12138/RazerBladeAdvanced2020_Hackintosh). I modified, cleaned and updated EFI from this repo. 

## Recommendations

In order to boot macOS on the Razer Blade, you need to change [UEFI BIOS Configuration](https://github.com/i4pptem/RazerBlade15-Base-2021-Hackintosh#uefi-bios-configuration).

Please be aware that all `PlatformInfo` and `SMBIOS` information was removed from the OpenCore `config.plist` files. Users will therefore need to generate their own `PlatformInfo` with [CorpNewt's GenSMBIOS tool](https://github.com/corpnewt/GenSMBIOS) before attempting to boot with this repository's EFI folder.

I added "-v debug=0x100 keepsyms=1" BootArgs, to debug, after installation you can clear bootarg's. If you can't boot, please check [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)

## Software Specifications
| Software         | Version                            |
| ---------------- | ---------------------------------- |
| OS               | macOS 14.2.1 Sonoma |
| OpenCore         | [OC v0.9.7](https://github.com/acidanthera/OpenCorePkg/releases/download/0.9.7/OpenCore-0.9.7-RELEASE.zip) |
| SMBIOS           | MacBookPro16,1 |
| BIOS             | v1.00 |

## Hardware Specifications
| Device           | Model  | Compatibility |
| ---------------- | ---------------------------------- | -----------|
| CPU              | Intel Core  i7-10750H 6-Core (2.6GHz / 5.0GHz) | No Issues |
| Chipset          | Intel HM470 | No Issues | 
| iGPU             | Intel UHD Graphics 630 | No Issues |
| dGPU             | NVIDIA GeForce RTX 3060 |Not working, disabled |
| Display          | BOEhydis NV156FHM-NY4 15.6 1080p 144Hz | No Issues |
| RAM              | 16GB Samsung DDR4 2933MHz | No Issues |
| Audio            | Realtek ALC298 | No Issues |
| WiFi | Intel Wi-Fi 6 AX201 160MHz | No Issues (not stable, probably because of Alpha version of kext) |
| Storage          | Samsung SSD 970 EVO Plus 1TB | No Issues |
| TouchPad         | Precision Glass | No Issues |
| Webcam           | HD webcam (1MP / 720P) | No Issues |
| Keyboard         | RGB Razer Chroma Backlit | No Issues, can't config color, no software |
| Port             | USB 3.1 | No Issues |
|                  | Thunderbolt 3 (USB-C) | No Issues, display connection not tested |
|                  | HDMI | Not working, dGPU connection |
| Battery          | Replaced 65Wh rechargeable lithium-ion polymer battery | No Issues, ~5 Hours of Video Playback on 50% brightness | 
| Power            | 230W Power Adapter | No Issues |

## What needs some more work
- [ ] Sleep by closing lid

## What will never work
- [ ] NVIDIA GeForce RTX 3060 dGPU (disabled with an SSDT)
- [ ] HDMI output (hardwired to the NVIDIA dGPU)
- [ ] Airdrop (WiFi Module need to be replaced)

## UEFI BIOS Configuration
Many other Razer Blade machines need to unlock the BIOS and change the SAC to work properly, but software Mod of BIOS is locked, it can be Modified only by hardware method.

* Reboot computer
* Repeatedly press the ``F1`` or ``DEL`` key to enter the UEFI BIOS configuration menu
* In the UEFI BIOS navigate to the menu
	* ``Advanced``
		* ``Power & Performance``
			* ``CPU - Configuration``
					* Disable ``Software Guard Extensions (SGX)``
					* Enable ``Intel (VMX) Virtualization Technology``
          * Enable ``Hyper-Threading``
	* ``Advanced``
		* ``Thunderbolt(TM) Configuration``
			* Switch ``Security Level`` to ``No Security``
  * ``Advanced``
		* ``Thrusted Computing``
			* Disable ``Secutiry Device Support``
	* ``Chipset``
		* ``SATA And RST Configuration``
			* Check ``SATA Mode Selection`` set to ``AHCI``
	* ``Security``
		* Set ``Secure Boot`` to ``Disabled``
	* ``Boot``
		* Set ``Fast Boot`` to ``Disabled``
		* ``CSM Configuration``
			* Set ``CSM Support`` to ``Disabled``
	* ``Save and Exit``
		* Hit ``Save Changes``
		* Hit ``Save Changes and Reset``
 
## Sound
If your audio is not working, try different ALC Layout ID, my work perfect with LayoutID=21, otherwise  try: 3, 11, 13, 16, 21, 22, 28, 29, 30, 32, 47, 66, 72, 99. The detailed ALC configuration can refer to here: __[AppleALC Supported Codecs](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs)__

## Sleep
Sleep working fine, if you go to sleep before closing lid, if you try sleep by closing lid, you will be wake in black screen.

## Conclusion
If your machine run in to any problems or malfunctions during installation, I will not be responsible for that, so use this EFI at your own risk! Good luck, have fun, share your success to others may be able to help a lot!

## Native HiDPI display settings in macOS
To enable native HiDPI settings in the Display Preferences of macOS, download and run the [one-key-hidpi](https://github.com/jlempen/one-key-hidpi) script and select the option `(1) 1920x1080 Display`.

## Caps-Lock Indicator
* Install [Karabiner-Elements](https://pqrs.org/osx/karabiner/)
* Enable ``Manipulate LED`` for ``Razer Blade (Razer)`` in ``Devices`` section

## Configuring the RGB of the keyboard
You can try config your keyboard backlight by [Razer macOS](https://github.com/1kc/razer-macos) utility, in my case this is not recognize my keyboard.

## Related repositories
* https://github.com/Japerz12138/RazerBladeAdvanced2020_Hackintosh
* https://github.com/Tyson-Hu/RazerBlade15-Base-Model-Hackintosh_macOS_Sonoma
