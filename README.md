# Aurora Glass v3 — animated dashboard card for Home Assistant

🇮🇹 [Leggi in italiano](README.it.md)

![Aurora Glass v3](docs/dashboard-casa-notte-intera.webp)

A single custom card that turns a Home Assistant dashboard into a living scene: the sky, sun, moon and the windows of the little house follow the real time of day, ten animated "worlds", eleven weather effects, buttons made of images and GIFs, alarm, climate, cameras and an energy view that shows costs in euro (or any currency) from your own tariff.

- **Live demo (no install):** https://domotikpro.it/aurora-glass-v3-demo/
- **Full illustrated guide (Italian):** https://domotikpro.it/progetti/aurora-glass-v3
- **Video walkthrough (Italian):** https://www.youtube.com/@domotikproit

| Tablet | Energy | Mobile |
|---|---|---|
| ![Tablet](docs/tablet-casa-tramonto.webp) | ![Energy](docs/energia-vista.webp) | ![Mobile](docs/mobile-casa-notte-sm.webp) |

## Features
- 10 animated worlds and 11 weather effects (rain, snow, storm, fireflies, petals, fireworks…)
- Sky that follows the real time of day
- 50 ready-made button images and GIFs (lights, scenes, sensors, alarm, climate)
- Alarm panel, climate control, cameras
- Energy view: power, kWh today/yesterday/month/year and cost = kWh × your tariff
- One JavaScript file, no build step, no cloud
- **Privacy:** everything runs locally. The only external request is Google Fonts (Manrope, Sora). No data is collected or sent anywhere.

## Install (about 10 minutes)
The commented, step-by-step version is in [`aurora-glass-v3/LEGGIMI.txt`](aurora-glass-v3/LEGGIMI.txt) (Italian). Short version:

1. **Copy the files.** Put the folder `aurora-glass-v3/www/aurora-v3` into the `www` folder of your Home Assistant configuration (File editor, Samba or Studio Code Server). Result: `www/aurora-v3/aurora-v3.js` and `www/aurora-v3/btn/…`. If `www` is new, restart Home Assistant once. Test: open `<your HA address>/local/aurora-v3/aurora-v3.js` in the browser — you should see text.
2. **Add the resource.** Profile → enable *Advanced mode*. Settings → Dashboards → ⋮ → Resources → Add resource: URL `/local/aurora-v3/aurora-v3.js?v=1`, type *JavaScript module*. Bump the number after `?v=` when you update the card.
3. **Create a dashboard.** Settings → Dashboards → Add dashboard → New dashboard from scratch.
4. **Paste the card.** Open the dashboard → pencil → ⋮ → *Raw configuration editor*, replace everything with [`dashboard-esempio.yaml`](aurora-glass-v3/dashboard-esempio.yaml) and save. Lights will be grey until you map your entities.
5. **Map your entities.** Developer tools → States: find your entity IDs and add them under `entities:` as shown in [`scheda-esempio.yaml`](aurora-glass-v3/scheda-esempio.yaml) (all options, commented).
6. **Energy (optional).** Set your power sensor (W) in `energy.power`. For daily/monthly/yearly kWh use [`aurora-energia.yaml`](aurora-glass-v3/aurora-energia.yaml). Tap the *Tariffa* bar in the Energy view and enter what you pay per kWh.

The card is named `custom:aurora-v3-card`. Comments in the YAML files and the guide are in Italian; the options are plain YAML keys.

## Troubleshooting
- *Red card "Custom element doesn't exist"* — check the resource URL and hard-refresh (Ctrl+F5).
- *Empty images* — `assets` must be `/local/aurora-v3/btn/` (with the trailing slash).
- *Grey lights* — the entity ID doesn't exist or the device is offline.
- *Costs at zero* — tap the *Tariffa* bar and set your price per kWh.

## Remove
Delete the dashboard, the resource and the folder `www/aurora-v3`. Nothing else is touched.

## Status
Version 3, tested on Home Assistant 2026.9 by the author. Issues and suggestions are welcome — please open an issue.

## License
Free to download and use at home, **unmodified**. Editing the example YAML to configure your own entities is fine; modifying or redistributing the card, code or images is not allowed without permission. Full terms in [LICENSE](LICENSE) (EN/IT). Permissions: richieste@domotikpro.it

---
Made by [DomotikPro.it](https://domotikpro.it) — practical guides for a reliable smart home.
