LUMA HOME for Home Assistant
====================================
Unofficial derivative of Aurora Glass v3.
Original project: © 2026 DomotikPro.it (Luca Pinelli).
Adaptation and translations: Fonkyup.
Guide updated October 26, 2026.

An animated dashboard: time-aware sky, 10 worlds, 11 weather effects, image and GIF
buttons, alarm, climate control, cameras, and energy tracking.
Interface available in French, English, and Italian.

MANUAL INSTALLATION CONVENTION
  Public name: Luma Home
  Card type: custom:luma-home-card
  JavaScript file: aurora-v3.js (filename retained)
  Home Assistant folder: www/luma-home/
  Images: /local/luma-home/btn/

These instructions describe the target layout after migrating to luma-home.
Do not change URLs alone: copy the files to the new location first.
Renaming a GitHub folder does not move files inside Home Assistant.

DOCUMENTS AND EXAMPLES
  README.en.txt                this guide
  dashboard-example.en.yaml    complete dashboard in English
  card-example.en.yaml         detailed card options in English
  aurora-energia.en.yaml       optional energy meters with English instructions
  LEGGIMI.txt                  Italian guide
  LISEZMOI.fr.txt              French guide

Examples must use custom:luma-home-card and /local/luma-home/btn/.
Entity IDs are examples to replace with those from your installation.
DomotikPro.it guides and demos concern the original project, not necessarily
Luma Home’s current installation paths and identifiers.

INSTALLATION IN SIX STEPS
1) COPY THE FILES
   Use aurora-v3.js and its complete btn folder from the translated version.
   The dist distribution contains the copy intended for distribution. Keep the
   JavaScript and images from the same version.
   Using File editor, Samba, or Studio Code Server, create:
       www/luma-home/aurora-v3.js
       www/luma-home/btn/...
   www belongs inside your Home Assistant configuration folder, which may be
   called /homeassistant in File editor. If www is new, restart Home Assistant once.
   Test: open <Home Assistant address>/local/luma-home/aurora-v3.js.
   JavaScript text should appear.

2) ADD OR UPDATE THE RESOURCE
   Profile -> enable Advanced mode.
   Settings -> Dashboards -> menu ⋮ -> Resources.
       URL: /local/luma-home/aurora-v3.js?v=1
       Type: JavaScript module
   Update an existing resource instead of adding a duplicate.
   Increase the number after ?v= when updating, then reload the browser.

3) CREATE THE DASHBOARD
   Settings -> Dashboards -> Add dashboard -> start from scratch.
   Suggested title: Luma Home; icon: mdi:home-heart.

4) PASTE THE CONFIGURATION
   Open the dashboard -> edit -> menu -> Raw configuration editor.
   Back up any existing configuration before replacing it.
   For a new dashboard, use dashboard-example.en.yaml and save.
   Do not paste card-example.en.yaml at the dashboard root: it describes one card,
   not a complete dashboard configuration.

5) SELECT THE LANGUAGE AND MAP ENTITIES
   In the card YAML editor, the minimal configuration is:

   type: custom:luma-home-card
   language: en
   assets: /local/luma-home/btn/

   language values: fr, en, it. Without this option, the current code uses Italian.
   Developer tools -> States: find your entity IDs.
   Add entities at the same level as type, language, and assets:

   entities:
     lights:
       salotto: light.salotto

   Replace light.salotto with your entity; retain the technical key salotto.
   See card-example.en.yaml for other options.

6) ENERGY AND RATE — OPTIONAL
   Configure the power sensor in entities.energy.power, in watts:

   entities:
     energy:
       power: sensor.potenza_casa

   Merge this into your existing entities section; do not duplicate the section.
   For kWh meters, use only ONE version of aurora-energia.yaml: Italian, French,
   OR English. Never install all three together.
   Replace sensor.SENSORE_ENERGIA_KWH with your cumulative energy sensor in kWh,
   not a power sensor in W. Preserve the meter identifiers.
   Check the Home Assistant configuration before restarting.
   Set your price per kWh in the Energy view. Estimated cost = kWh × rate.
   Dividing an entire bill by kWh gives an average cost including any fixed fees;
   it is not necessarily the actual variable unit rate.

MIGRATING AN EXISTING INSTALLATION
 - Back up the working JavaScript and YAML.
 - Copy files into www/luma-home/ before changing references.
 - Update the resource, card type, and assets together.
 - Test JavaScript, images, languages, and commands before removing the old folder.
 - Do not remove resources or folders still used by another dashboard.

HACS
 These /local/ paths describe a manual installation. For HACS, use the actual
 installed paths; do not blindly replace /hacsfiles/ URLs.
 In hacs.json, filename remains aurora-v3.js while the file retains that name.
 Passing HACS validation does not automatically publish the project in its catalog.

TROUBLESHOOTING
 - “Custom element doesn't exist”: check the loaded file and custom:luma-home-card.
 - Missing images: check www/luma-home/btn/ and assets, including the trailing slash.
 - Grey lights: check entity IDs and availability.
 - Zero costs: check sensors and the rate.
 - Old language or text: check language, increase ?v=, and reload.

PRIVACY
 According to the original documentation, the card runs locally and loads the
 Manrope and Sora Google Fonts. The original author states that it does not collect
 or send data. This is not an independent network-traffic audit.
 Device integrations may have their own external connections.

UNINSTALLING
 Remove the relevant dashboard, resource, and www/luma-home/ only when nothing
 else uses them. These steps do not automatically remove browser preferences
 or energy sensors configured separately.

LICENSE AND ATTRIBUTION
 Luma Home is an unofficial derivative; no original-author endorsement is claimed.
 Original credit preserved: © 2026 DomotikPro.it (Luca Pinelli).
 Adaptation and translations: Fonkyup.

 The derivative software is distributed under GNU GPL version 3. You may use,
 modify, and redistribute it, including commercially, subject to the license.
 Distributed versions must, among other requirements, preserve applicable notices,
 identify modifications and their dates, and meet licensing and Corresponding Source
 obligations. Separate third-party component terms may remain applicable.
 Aurora Glass and DomotikPro.it identify the original project; no trademark rights
 or endorsement are claimed.

 See LICENSE at the repository root for the full terms. Do not modify the GPL text.
 This guide does not replace it. The software is provided without warranty to the
 extent stated in the license and permitted by applicable law.
