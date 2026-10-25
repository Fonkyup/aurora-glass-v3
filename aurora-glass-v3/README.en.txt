AURORA GLASS v3 for Home Assistant
====================================
The animated dashboard: a sky that changes with the time of day, 10 worlds, 11 weather effects,
buttons made from images and GIFs, an alarm, climate control, cameras, and energy tracking with costs in euros.

FULL GUIDE WITH SCREENSHOTS: on the website’s “Guide” page (and in the YouTube video).
Below is a summary in 6 steps (about 10 minutes).

CONTENTS
  README.en.txt               this file, translated into English
  dashboard-esempio.yaml      the dashboard, ready to copy and paste
  scheda-esempio.yaml         ALL card options, with comments
  aurora-energia.yaml         daily/monthly/yearly kWh meters (optional)
  www/aurora-v3/aurora-v3.js   the card (a single file)
  www/aurora-v3/btn/           50 button images and GIFs

STEPS
1) COPY THE FILES
   Place the www/aurora-v3 folder inside Home Assistant’s www folder
   (using File editor, Samba, or Studio Code Server). The result should be:
       www/aurora-v3/aurora-v3.js
       www/aurora-v3/btn/...
   In the File editor add-on, the configuration folder is called /homeassistant:
   it is the same folder. If you have just created www, restart Home Assistant once.
   Test: open <Home Assistant address>/local/aurora-v3/aurora-v3.js in your browser.
   If text appears, everything is in place.

2) ADD THE RESOURCE
   Profile -> enable “Advanced mode”.
   Settings -> Dashboards -> menu (three dots) -> Resources -> Add resource
       URL:   /local/aurora-v3/aurora-v3.js?v=1
       Type:  JavaScript module
   (When updating the card, increase the number after ?v=.)

3) CREATE THE DASHBOARD
   Settings -> Dashboards -> Add dashboard -> Create a new dashboard from scratch
   Title: “Aurora”; icon: mdi:home-heart; enable “Show in sidebar”.

4) PASTE THE CARD CONFIGURATION
   Open the dashboard -> pencil -> menu -> “Raw configuration editor”.
   Delete everything and paste the contents of dashboard-esempio.yaml -> Save.
   The lights will be greyed out: the names are examples.

5) CONNECT YOUR ENTITIES
   Developer tools -> States: look up the names (light., binary_sensor., ...).
   Below “assets:”, add the “entities:” section with your entity names
   (see scheda-esempio.yaml: it contains all the options).

6) ENERGY AND RATE (optional)
   Specify your power sensor (W) in energy.power: the Energy view appears.
   For today’s, yesterday’s, monthly, and yearly kWh, use aurora-energia.yaml.
   In the Energy view, tap the “Rate” bar and enter how much you pay per kWh
   (or calculate it from your bill: total amount due / kWh).
   From then on, each cost is calculated as kWh × rate.

TROUBLESHOOTING
 - Red card showing “Custom element doesn't exist”: check the resource and reload with Ctrl+F5.
 - Missing images: “assets” must be /local/aurora-v3/btn/ (with the trailing slash).
 - Greyed-out lights: the entity name does not exist or the device is offline.
 - Costs showing zero: tap the Rate bar.

PRIVACY
 Everything runs locally. The only external requests are for Google Fonts (Manrope, Sora).
 No data is collected or sent.

UNINSTALLING
 Delete the “Aurora” dashboard, the resource, and the www/aurora-v3 folder.
 Nothing else is changed.

Aurora Glass v3 — free for personal use, to be used without modifications
(the example YAML files may be modified).
GPL-3.0 license: you may use, modify, and share the card, including for commercial
purposes, provided that modified versions remain under GPL-3.0, with the source
code and a name other than “Aurora Glass”. See LICENSE.
