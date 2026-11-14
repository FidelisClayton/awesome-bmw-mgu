# Awesome BMW MGU [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Community apps, tools and guides for BMW head units running the MGU (iDrive 7 and iDrive 8), with a safety label on every entry.

**Unofficial.** Nothing here is made, endorsed or supported by BMW AG. Rooting and modding a head unit is at your own risk: it can reset the car's coding, remove Digital Key pairings and, in the worst case, leave the head unit unusable. Read [Start here safely](#start-here-safely) before you install anything.

Labels were checked against each project's own README and manifests on **2026-11-06**, and EQ Config on **2026-11-14**. Projects change fast, so read the repository before you install.

## Contents

- [Start here safely](#start-here-safely)
- [Labels](#labels)
- [Root access](#root-access)
- [App store](#app-store)
- [Instrument cluster and HUD](#instrument-cluster-and-hud)
- [Driving data and diagnostics](#driving-data-and-diagnostics)
- [Media and streaming](#media-and-streaming)
- [Games](#games)
- [Vehicle functions](#vehicle-functions)
- [System tweaks](#system-tweaks)
- [Setup helpers](#setup-helpers)
- [Hardware](#hardware)
- [App development](#app-development)
- [iDrive 8](#idrive-8)
- [Regional](#regional)
- [Forks with their own features](#forks-with-their-own-features)
- [Caution](#caution)
- [Not for MGU](#not-for-mgu)
- [Related](#related)

## Start here safely

1. **Back up the head unit's coding before you root it.** Rooting with [idrive7-8-ssh-root](https://github.com/cauliflowermossgrape/idrive7-8-ssh-root) flashes a debug image, and the flash wipes the head unit's coding (CAFD) and its BMW Digital Key pairings. Save the coding with BimmerCode, E-Sys or ISTA first.
2. **If settings reset, tiles disappear or the touchscreen stops responding after rooting, restore the coding.** Use the BimmerCode backup, or recode `HU_MGU` with E-Sys from the saved NCD. Do not re-flash: the flash is what cleared it. In [one reported case](https://github.com/cauliflowermossgrape/idrive7-8-ssh-root/issues/40) a dead touchscreen after rooting was a coding issue, and restoring the BimmerCode backup brought it back.
3. **Install through the [MGU Store](https://github.com/robertnisipeanu/mgu-store).** It backs up what it changes and can remove everything it installed.
4. **Prefer apps to root tools from authors you don't know.** A root tool runs as root on the head unit.
5. **Before you drive with anything that redraws the cluster, check that BMW's warning lights still show.** For example, start the car with the seat belt unbuckled.
6. **Know your undo.** In the Store, remove the app, then its tools. `mgu-install.js uninstall` takes the whole Store setup off. Some tools have their own revert, such as `woc-patch.sh revert` for Waze on cluster.

## Labels

| Label | Meaning |
|---|---|
| `📱 app` | An OAP app on the head unit's app platform |
| `🔓 root tool` | Installs a tool that runs as root on the head unit |
| `✍️ changes the car` | Patches BMW programs, writes coding or sends commands to the car's control units |
| `🌐 internet` | Needs an internet connection in the car |
| `🚗 car-tested` | Its README says it ran on a real car (which car, where it says) |
| `🧪 not car-tested` | Bench, emulator or PC only, per its README |
| `❓ untested?` | Its README doesn't say whether it ran on a car |
| `📦 no source` | Ships packages without the source in the repository |
| `ID7` `ID8` | iDrive 7 / iDrive 8 support |

## Root access

- [cauliflowermossgrape/idrive7-8-ssh-root](https://github.com/cauliflowermossgrape/idrive7-8-ssh-root) - Root SSH on MGU head units (iDrive 7, ID8 BDC3, ID8 BCP) over an ENET cable: flashes a debug image once, enrolls an SSH key and keeps SSH across reboots. The flash wipes coding (CAFD) and Digital Key pairings, so back up first, and never re-flash to fix coding. `✍️ changes the car` `🚗 car-tested` `ID7` `ID8`

## App store

- [robertnisipeanu/mgu-store](https://github.com/robertnisipeanu/mgu-store) - An app store on the car's screen that installs, updates and removes apps and tools from GitHub repositories, web addresses or USB sticks. A computer installs it once over SSH, and it adds a renderer, an updater, an internet uplink (USB, LTE, phone or Wi-Fi) and app privacy. iDrive 8 is tested in an emulator only. `🔓 root tool` `📱 app` `🚗 car-tested` `ID7` `ID8`

## Instrument cluster and HUD

- [robertnisipeanu/idrive-apps](https://github.com/robertnisipeanu/idrive-apps) - `cluster-render`, the shared renderer other apps use to draw on the instrument cluster and the HUD, plus **Waze on cluster**, which shows the CarPlay (or Android Auto) map on the cluster as video. Waze on cluster patches the CarPlay program, keeping a backup and recovering at boot. Its install patches only the proven CarPlay build and leaves any other build alone. `🔓 root tool` `✍️ changes the car` `🚗 car-tested` `ID7`
- [bimmer-lab/apps](https://github.com/bimmer-lab/apps) - **Cluster Themes** redraws the whole cluster as a GT3 race dash, an M-style cluster or a Sport view, and can follow the drive mode buttons. **HUD Widgets** puts speed, gear, shift lights, boost and temperatures on the HUD. Still to be checked on the car: whether BMW's warning lights show over the themes. `📱 app` `🚗 car-tested` (2020 X3 M40i) `ID7`
- [isaakbruno2/carplay-map-cluster](https://github.com/isaakbruno2/carplay-map-cluster) - Copies the CarPlay map you see onto the cluster through cluster-render (about 6 fps), with no patch and no modified BMW programs. Made for CarPlay builds where Waze on cluster's patch refuses. Installed with a script on the head unit, not from the Store. `🔓 root tool` `🚗 car-tested` (2020 G20 320i) `ID7`
- [kxrxh/bmw-clusters-mgu](https://github.com/kxrxh/bmw-clusters-mgu) - S2000 and BMW M instrument clusters in one app, drawn in code. Turn off the older separate S2000 Cluster and BMW M Cluster apps first. Russian README. `📱 app` `❓ untested?` `ID7`
- [eroobeeroo/idrive7-apps](https://github.com/eroobeeroo/idrive7-apps) - **Cluster Info** puts a small panel of live values (oil and coolant temperature, boost, rpm, torque) over the Waze map on the cluster or HUD, plus turn-signal arrows on the HUD. Also **eDrive Live** for plug-in hybrids, and **Light Show**, which plays patterns on the exterior lights through the body controller's lamp tests. It carries only these apps; the rest come from idrive7-apps. `📱 app` `🔓 root tool` `✍️ changes the car` `🚗 car-tested` (2021 X5 xDrive45e G05) `ID7`
- [PenguinDukeYDAuto/idrive7-EVAHUD](https://github.com/PenguinDukeYDAuto/idrive7-EVAHUD) - A NERV-style (Evangelion) HUD and cluster app, built on bimmer-lab/apps, idrive7-apps and idrive-apps. Chinese and English README. `📱 app` `❓ untested?` `ID7`
- [cruzen991/Cluster](https://github.com/cruzen991/Cluster) - Classic round dials over the stock gauges (speedometer, tachometer with boost and oil temperature, gear window) in Tech, Sport and Classic styles, with shift lights. The stock gauges are hidden while the dials are on. `📱 app` `🧪 not car-tested` (PC only) `ID7`
- [sergshamiryan/mgu-gear-cluster](https://github.com/sergshamiryan/mgu-gear-cluster) - Shows the gear (D1 to D8) on the cluster. Installs from the Store or from a USB stick. `📱 app` `❓ untested?` `ID7`
- [JustAnotherPU/waze-hud](https://github.com/JustAnotherPU/waze-hud) - Waze's next turn on BMW's own HUD arrows (read from the CarPlay picture), plus the map on the cluster. It is an alternative to Waze on cluster: both patch CarPlay, so install only one. `🔓 root tool` `✍️ changes the car` `🚗 car-tested` (one X5 G05) `ID7`
- [Vizualyse/idrive-apps](https://github.com/Vizualyse/idrive-apps) - **Cast to cluster** puts a stream from your phone on the cluster, the HUD or the centre screen, and gets CarPlay's cluster map through a hook preloaded into CarPlay. Also **Moonlight** game streaming. A tech demo. `🔓 root tool` `✍️ changes the car` `🧪 not car-tested` (bench unit) `ID7`
- [Impossible43/vlad-mgu-apps](https://github.com/Impossible43/vlad-mgu-apps) - An experimental mirror of the CarPlay Dashboard map. Version 0.1.0 worked on an X3 G01 apart from layout detection and scaling. `📱 app` `🚗 car-tested` (partly) `ID7`
- [noth4m4d/mgu-hamadstools](https://github.com/noth4m4d/mgu-hamadstools) - AirPlay screen mirroring and Waze Cards. The picture is hidden while driving by default. `🔓 root tool` `📱 app` `❓ untested?` `ID7`

## Driving data and diagnostics

- [cauliflowermossgrape/idrive7-apps](https://github.com/cauliflowermossgrape/idrive7-apps) - The best-known collection: Redline shift lights, Virtual Dyno, brake and drag timers, G-Force, M Vitals, Warm-Up, eDrive, Live Data, Service, a ZF 8HP gearbox page, a Fault Scanner that can clear fault memories, and Doom. Through the Store it also installs its own GPU renderer and the controller input gate, which loads into the HMI. `📱 app` `🔓 root tool` `🚗 car-tested` `ID7`
- [aurelmarius/bmw-apps](https://github.com/aurelmarius/bmw-apps) - **Engine Care** tracks how often a plug-in hybrid starts its engine cold, from the engine unit's diagnostic data. Also **Hybrid Cost**. `📱 app` `❓ untested?` `ID7`
- [arefahmad/idrive7-apps](https://github.com/arefahmad/idrive7-apps) - Read-only apps: Car Care, a Drive Log calibrated against a Dragy, Fault Watch, Car Lyrics and an explorer. `📱 app` `🧪 not car-tested` `ID7`
- [pinguinooo/idrive7-apps](https://github.com/pinguinooo/idrive7-apps) - M Track, shift lights and Vitals. Each app's README says what has run on a car and has a Safety section. `📱 app` `ID7`
- [JustAnotherPU/mgu-apps](https://github.com/JustAnotherPU/mgu-apps) - iDrive Monitor, a system monitor for the head unit, plus Tailscale and Node.js 22 as tools. `📱 app` `🔓 root tool` `🚗 car-tested` (X5 xDrive45e G05) `ID7`
- [benspa900/mon-vitals-idrive7](https://github.com/benspa900/mon-vitals-idrive7) - A personal dashboard built on M Vitals. Demo data stays off unless you switch it on. French README. `📱 app` `❓ untested?` `ID7`
- [dzooky/bmrmodz](https://github.com/dzooky/bmrmodz) - An Oil Service Assistant (engine and gearbox oil temperatures for service procedures, read-only), built on the idrive7-apps kit. DPF tools are still being built. `📱 app` `🔓 root tool` `❓ untested?` `ID7`
- [nickgcode/idrive7-apps](https://github.com/nickgcode/idrive7-apps) - G's Dash (with a Spotify panel), G's Music and G's TV (channels from the Internet Archive), with optional picks on the cluster and HUD. `📱 app` `🌐 internet` `❓ untested?` `ID7`

## Media and streaming

Several of these can be set to keep playing while the car moves. That is for passengers only: the driver must never watch the screen, and it may be illegal where you drive.

- [timokhin/id7-eq-config](https://github.com/timokhin/id7-eq-config) - **EQ Config** adjusts sound profiles, balance, fade and surround on the head unit. Tested with ID7 + Harman Kardon. `📱 app` `🚗 car-tested` `ID7`
- [hexlay/idrive7-custom-apps](https://github.com/hexlay/idrive7-custom-apps) - A Spotify Connect controller and library browser for the centre screen, and **M Copilot**, which answers questions about the car from 24 topics (health check, warning lights and faults, service and more). Its BDC coding tool is not offered yet. `📱 app` `🌐 internet` `❓ untested?` `ID7`
- [JustAnotherPU/ridetube](https://github.com/JustAnotherPU/ridetube) - An unofficial YouTube client with TV sign-in, subscriptions and Watch later. While driving it switches to a podcast view. `📱 app` `🔓 root tool` `🌐 internet` `🚗 car-tested` (X5 xDrive45e G05) `ID7`
- [JustAnotherPU/ridewatch](https://github.com/JustAnotherPU/ridewatch) - Home cameras (UniFi Protect, any RTSP camera) on the centre screen, parked only by default. Its stream is unencrypted, so don't expose its port to the internet. `📱 app` `🔓 root tool` `🌐 internet` `❓ untested?` `ID7`
- [JustAnotherPU/moonride](https://github.com/JustAnotherPU/moonride) - Moonlight game streaming from a PC to the centre screen at 60 fps, with car audio and USB controllers. Parked only by default, with 5G play over Tailscale. `📱 app` `🔓 root tool` `🌐 internet` `🚗 car-tested` (X5 xDrive45e G05) `ID7`
- [pllanaio/mgu-browser](https://github.com/pllanaio/mgu-browser) - An experimental Chromium browser with controller navigation and tabs. An earlier version ran on the author's own iDrive 7 head unit; the current package, audio, DRM and touchpad gestures are not checked yet. German README. `📱 app` `🔓 root tool` `🌐 internet` `❓ untested?` `ID7`
- [Drake1804/bube-releases](https://github.com/Drake1804/bube-releases) - A personal YouTube player. The source ships as tarballs in its releases. `📱 app` `🔓 root tool` `🌐 internet` `❓ untested?` `ID7`

## Games

- [aurelmarius/bmw-games](https://github.com/aurelmarius/bmw-games) - Eleven games drawn on the GPU at 60 fps (pinball, solitaire, snake, blackjack, a top-down racer, an arcade shooter and more). All parked only, with play credits only. `📱 app` `❓ untested?` `ID7`
- [iAbadia/idrive-games](https://github.com/iAbadia/idrive-games) - Games built for the iDrive controller, starting with 2048 with animated tiles, saved progress and high scores. `📱 app` `❓ untested?`
- [kxrxh/doodle-jump-mgu](https://github.com/kxrxh/doodle-jump-mgu) - Doodle Jump. Needs the controller input gate. `📱 app` `🔓 root tool` `🧪 not car-tested` (emulator)
- [mistergahan/mgu-backgammon](https://github.com/mistergahan/mgu-backgammon) - Short and long backgammon (nardy), two players or against the computer. Russian README. `📱 app` `🧪 not car-tested`

## Vehicle functions

These send commands to the car's control units or change its coding. They carry more risk than apps that only read.

- [evangoyuk/mgu-store-apps](https://github.com/evangoyuk/mgu-store-apps) - Gentleman Function, the exhaust flap and Start/Stop, and Shift Lights. Prebuilt packages in its releases, built with the idrive7-apps kit. `📱 app` `✍️ changes the car` `📦 no source` `❓ untested?` `ID7`
- [sembsa/idrive7-ambient](https://github.com/sembsa/idrive7-ambient) - Ambient light experiments through the car's comfort-function service. `📱 app` `✍️ changes the car` `❓ untested?`
- [NamelsMissing/mgu-apps](https://github.com/NamelsMissing/mgu-apps) - G21 ambient light and steering-wheel heating, with safety checks before each command, plus a custom cluster, a DPF monitor, game apps, a video hub and a phone terminal, and a `phone-bridge` tool. Its README says some parts are not verified on a car yet. `📱 app` `🔓 root tool` `✍️ changes the car` `🌐 internet` `❓ untested?`
- [istt1899/x3](https://github.com/istt1899/x3) - A coding catalogue and read-only control-unit discovery for the X3 (G01), as a Store source. Russian README. `✍️ changes the car` `❓ untested?`

## System tweaks

- [MareXcodemaster/idrive7-carplay-multitouch](https://github.com/MareXcodemaster/idrive7-carplay-multitouch) - Multitouch for the factory CarPlay, for one exact MGU software build. It builds a patched copy of CarPlay from the one on your head unit, leaves `/usr/bin/carplay` untouched and adds a reversible service override. Windows installer with a verified backup and removal. `🔓 root tool` `✍️ changes the car` `🚗 car-tested` (one software build) `ID7`

## Setup helpers

Programs that run on your computer, not on the car.

- [Wallezy/mgu-setup-skills](https://github.com/Wallezy/mgu-setup-skills) - A bilingual skill for AI coding agents covering owner-authorised MGU setup and maintenance: ENET and root SSH, backups, installing the Store.
- [IvanBiondi/mgu-assistant](https://github.com/IvanBiondi/mgu-assistant) - A Windows assistant: ENET checks, guided SSH setup and offline Store installation. Experimental; its tests don't cover a real car.
- [nic0pane/mgu-unified-manager](https://github.com/nic0pane/mgu-unified-manager) - A desktop app (Tkinter) that coordinates idrive7-8-ssh-root and the MGU Store.
- [Viaszx/BMW_HU_Info](https://github.com/Viaszx/BMW_HU_Info) - A Windows program that reads detailed information from NBT EVO, MGU and ENAVEVO head units.

## Hardware

- [rishik250809/bmw-idrive-controller](https://github.com/rishik250809/bmw-idrive-controller) - An Arduino sketch and a browser page that emulate the iDrive controller on the CAN bus, to drive a head unit on the bench or add your own controls. For iDrive 6, 7 and 8. `ID7` `ID8`

## App development

- [idrive7-apps SDK kit](https://github.com/cauliflowermossgrape/idrive7-apps#readme) - Build your own apps: extract the SDK from your own head unit, build, and try them in a live emulator on your computer. Never publish packages that contain BMW's SDK.
- [Publishing for the MGU Store](https://github.com/robertnisipeanu/mgu-store/blob/main/docs/PUBLISHING.md) - Release, catalog and repo-tree layouts, ids, `mguHmi`, requirements.
- [cluster-render](https://github.com/robertnisipeanu/idrive-apps/tree/main/native/cluster-render) - The protocol and Node and C++ clients for drawing layers on the cluster and HUD from your own app.

## iDrive 8

- [IterioDev/car-apps](https://github.com/IterioDev/car-apps) - Car Data, Drag Timer, Drive Recorder, eDrive, Fault Codes, Live Adjustments, Overlays (shortcuts, seat and wheel heating buttons, shift lights on the cluster and HUD), Service, Tailscale and screen sharing. Almost all are iDrive 8 only and not tested on iDrive 7; Drive Recorder also runs on iDrive 7 (tested on one G20). `📱 app` `🔓 root tool` `✍️ changes the car` `🚗 car-tested` `ID8`
- [rishik250809/idrive8-app-test](https://github.com/rishik250809/idrive8-app-test) - A minimal iDrive 8 app to start from. `🧪 not car-tested` (bench, MGU21) `ID8`

## Regional

- [istt1899/bmw-kaluga-cameras](https://github.com/istt1899/bmw-kaluga-cameras) - Offline speed-camera alerts for the Kaluga region (Russia). Experimental. `📱 app` `🔓 root tool` `❓ untested?` `ID7`
- [jaimeen77-cmyk/idrive7-korean-patch](https://github.com/jaimeen77-cmyk/idrive7-korean-patch) - A Korean translation (1,774 strings) for an older idrive7-apps version, applied to the source before building. Newer idrive7-apps versions build Korean themselves with `--language ko`. Korean README.

## Forks with their own features

Forks and copies are listed only when they say what they add. Plain copies are left out: install the original.

- [DimonPrograms/dimonprograms-apps](https://github.com/DimonPrograms/dimonprograms-apps) - Adds **Track Mode** (a lap timer with sectors, best lap and delta) and **Battery & Electrical** (12 V voltage, current, charge and health, read-only) to its own copies of the idrive7-apps set. Its app ids start with `dimon_`, so it can be added next to the original. Russian README. `📱 app` `🔓 root tool` `✍️ changes the car` `❓ untested?` `ID7`
- [DarkMuse1/idrive7-apps-ru](https://github.com/DarkMuse1/idrive7-apps-ru) - A Russian build of idrive7-apps that adds an ambient light app and an all-in-one "MGU Tools" app. It still ships AA Cluster Companion, which upstream removed as incompatible with the current Android Auto cluster map. Russian README. `📱 app` `🔓 root tool` `✍️ changes the car` `❓ untested?` `ID7`
- [kern4466/mgu-store-ua](https://github.com/kern4466/mgu-store-ua) - A fork of the MGU Store whose updater still downloads over HTTPS when the head unit's clock is wrong, through a downloader that checks certificates against NTP time. It replaces the Store's updater and uplink with its own older versions. Russian README. `🔓 root tool` `❓ untested?` `ID7`
- [eroobeeroo/idrive-apps](https://github.com/eroobeeroo/idrive-apps) - The Waze map on the HUD instead of the cluster. Upstream Waze on cluster has this now (Show on), so install the upstream version. `🔓 root tool` `✍️ changes the car` `🚗 car-tested` (2021 X5 xDrive45e G05) `ID7`

## Caution

- [mlurker/bmw-idrive7-releases](https://github.com/mlurker/bmw-idrive7-releases) - Android Auto's cluster map and HUD tools, as packages with no source in the repository. Its catalog publishes `cluster-render` and `waze-on-cluster` under the same ids as robertnisipeanu/idrive-apps, as its own builds at version `10.10.10`. Adding this source can replace those root tools with packages that can't be reviewed. Tested only on an X5 G05. `🔓 root tool` `✍️ changes the car` `📦 no source` `ID7`

## Not for MGU

- [BimmerGestalt/AAIdrive](https://github.com/BimmerGestalt/AAIdrive) - Android Auto features as BMW Connected Apps for older NBT and NBT EVO head units (no root needed). It does not support MGU.

## Related

- [awesome-bmw-coding](https://github.com/byakku/awesome-bmw-coding) - Coding, ECU programming and other BMW resources.
- [Custom native iDrive 7 apps](https://g20.bimmerpost.com/forums/showthread/2260780/custom-native-idrive-7-apps/page/2) - The Bimmerpost forum thread.

## Contributing

Additions and corrections are welcome. Read the [contribution guidelines](CONTRIBUTING.md) first: every entry needs its labels, checked against the project itself.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work.
