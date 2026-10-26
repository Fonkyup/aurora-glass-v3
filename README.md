# Luma Home — Multilingual dashboard for Home Assistant

[English](README.md) | [Français](README.fr.md) | [Italiano](README.it.md)

An unofficial derivative of Aurora Glass v3, adapted by Fonkyup with a French, English, and Italian interface.

> Current naming: the card type is `custom:luma-home-card`. The JavaScript filename remains `aurora-v3.js`. For the manual installation described below, files are installed in `www/luma-home/`. The source folder in this repository still uses `luma-home/www/aurora-v3/`; copy its contents into the installation folder rather than assuming both folder names must match.

![Interface inherited from Aurora Glass v3, the original project](docs/dashboard-casa-notte-intera.webp)

A custom card that turns a Home Assistant dashboard into a living scene: the sky, sun, moon, and the windows of the little house follow the real time of day. Ten animated worlds, eleven weather effects, buttons made from images and GIFs, an alarm, climate control, cameras, and an Energy view calculating costs from your own rate.

## Origin and contributions

This version is based on Aurora Glass v3, created by DomotikPro.it (Luca Pinelli).

Original notice preserved: © 2026 DomotikPro.it (Luca Pinelli).

Adaptation and translations: Fonkyup.

Contributions include:
- French and English interface translations;
- adaptation of interface text and dynamic messages;
- translated installation guides and configuration examples;
- adoption of the Luma Home public name and `custom:luma-home-card` identifier;
- documentation of the manual installation layout.

The original Italian language is retained. This version is not an official release and is not presented as endorsed by DomotikPro.it or Luca Pinelli.

Documentation updated on October 26, 2026. Modification dates are also recorded in source notices and the repository history.

The screenshots below come from the original project; they do not demonstrate validation of every translation.

| Tablet | Energy | Mobile |
|---|---|---|
| ![Tablet](docs/tablet-casa-tramonto.webp) | ![Energy](docs/energia-vista.webp) | ![Mobile](docs/mobile-casa-notte-sm.webp) |

## Original project resources

These links refer to Aurora Glass v3, not necessarily to this derivative:
- [Original live demo, in Italian](https://domotikpro.it/aurora-glass-v3-demo/index.html)
- [Original illustrated guide, in Italian](https://domotikpro.it/progetti/aurora-glass-v3)
- [Original author's videos, in Italian](https://www.youtube.com/@domotikproit)
- [Original repository](https://github.com/lucalux00/aurora-glass-v3)

The original project's installation paths and card identifiers may differ from those used by Luma Home.

## Features

Features inherited from the original project:
- 10 animated worlds and 11 weather effects: rain, snow, storms, fireflies, petals, fireworks…
- A sky that follows the real time of day.
- 50 ready-made button images and GIFs for lights, scenes, sensors, alarm, and climate.
- Alarm panel, climate control, and cameras.
- Energy view: power, kWh for today, yesterday, the month, and the year; cost calculated as kWh × rate.
- A card distributed as one JavaScript file, with no build step required for installation.

Added in this version: interface language selection using `language: fr`, `language: en`, or `language: it`.

## Privacy and connections

According to the original documentation, the card runs locally and loads the Manrope and Sora Google Fonts through an external request. The original author states that the card does not collect or send data.

This description is not a security or network-traffic audit. The Home Assistant integrations used for your devices may have their own external connections.

## Installation guides and examples

Short installation guides:
- [English](luma-home/README.en.txt)
- [Français](luma-home/LISEZMOI.fr.txt)
- [Italiano](luma-home/LEGGIMI.txt)

English configuration examples:
- [Complete dashboard](luma-home/dashboard-example.en.yaml)
- [Detailed card options](luma-home/card-example.en.yaml)
- [Optional energy meters](luma-home/aurora-energia.en.yaml)

These examples must use `custom:luma-home-card`. Their manual-installation image path should match the location described below.

## Manual installation

### 1. Copy the files

From `luma-home/www/aurora-v3/` in this repository, copy `aurora-v3.js` and the complete `btn` folder into a folder named `luma-home` inside your Home Assistant configuration's `www` folder.

The required installation layout is:

```text
www/
└── luma-home/
    ├── aurora-v3.js
    └── btn/
        └── button images and GIFs
```

The source and destination are deliberately different:

```text
Repository source:
luma-home/www/aurora-v3/aurora-v3.js

Home Assistant destination:
www/luma-home/aurora-v3.js
```

Use the JavaScript and images from the same version. The `dist` folder contains the distribution copy; do not mix files from different revisions.

If you have just created `www`, restart Home Assistant once.

Open this address in your browser:

```text
<Home Assistant address>/local/luma-home/aurora-v3.js
```

JavaScript text should appear.

### 2. Add or update the resource

Enable Advanced mode in your profile.

Settings → Dashboards → menu ⋮ → Resources:

- URL: `/local/luma-home/aurora-v3.js?v=1`
- Type: JavaScript module.

If the resource already exists, update it rather than adding a duplicate.

Increase the number after `?v=` when updating, then fully reload the browser. Avoid loading multiple versions of the same card.

### 3. Create the dashboard

Settings → Dashboards → Add dashboard → New dashboard from scratch.

Suggested title: `Luma Home`.

### 4. Paste the dashboard configuration

Open the dashboard → pencil → menu ⋮ → Raw configuration editor.

On a new dashboard, paste the contents of the [English dashboard example](luma-home/dashboard-example.en.yaml) and save.

Back up an existing dashboard configuration before replacing it.

The detailed card example describes a single card, not an entire dashboard. Do not paste it directly at the dashboard configuration root.

Lights may remain greyed out until you configure your own entities.

### 5. Choose the language and map your entities

The minimal card configuration for this manual installation is:

```yaml
type: custom:luma-home-card
language: en
assets: /local/luma-home/btn/
```

Supported language values:
- `en`: English;
- `fr`: French;
- `it`: Italian.

Without a language option, the current code defaults to Italian.

Developer tools → States: find your entity IDs.

Add `entities` at the same level as `type`, `language`, and `assets`:

```yaml
type: custom:luma-home-card
language: en
assets: /local/luma-home/btn/

entities:
  lights:
    salotto: light.salotto
```

Replace `light.salotto` with your actual entity ID. Keep technical configuration keys such as `salotto`, `cucina`, and `ingresso`: translating the interface does not rename these keys.

See the [detailed card example](luma-home/card-example.en.yaml) for the other options.

### 6. Configure energy — optional

Configure your power sensor, in watts, under `entities.energy.power`:

```yaml
type: custom:luma-home-card
language: en
assets: /local/luma-home/btn/

entities:
  energy:
    power: sensor.potenza_casa
```

Replace `sensor.potenza_casa` with your sensor. Merge this into your existing `entities` section rather than creating a duplicate section.

For energy-consumption meters in kWh, see the [English energy configuration](luma-home/aurora-energia.en.yaml).

Use only one language variant of the energy configuration: Italian, French, or English. They define the same meters and must not be installed together.

Replace the placeholder energy source with your cumulative energy sensor in kWh, not a power sensor in watts. Preserve the meter identifiers unless you also update all references.

Check your Home Assistant configuration before restarting.

In the Energy view, open the rate settings and enter your price per kWh. Displayed costs are estimates calculated from the configured consumption readings and rate.

Dividing an entire bill by kWh gives an average cost that may include fixed fees; it is not necessarily the actual variable unit rate.

## Migrating an existing installation

Before moving from the old installation layout:

1. Back up the working JavaScript and dashboard YAML.
2. Copy the JavaScript and images into `www/luma-home/`.
3. Update the existing resource to `/local/luma-home/aurora-v3.js?v=…`.
4. Change the card type to `custom:luma-home-card`.
5. Set `assets: /local/luma-home/btn/`.
6. Reload the browser and test images, languages, and commands.
7. Remove the old resource or folder only when nothing else uses it.

Renaming folders in this repository does not move files inside Home Assistant.

Do not rename energy sensor IDs or browser-storage keys as part of this file-path migration.

## HACS

The original project's HACS instructions use `lucalux00/aurora-glass-v3`. That installs the original project, not this adaptation.

The HACS validation workflow has passed during development. Passing validation does not automatically publish this derivative in the HACS catalog or prove that every installation scenario works.

A complete HACS installation and update test for this derivative remains a separate release check.

The `/local/luma-home/` paths above describe manual installation. For a HACS installation, use the actual installed paths; do not blindly replace `/hacsfiles/` URLs with manual-installation URLs.

The distributed JavaScript is `dist/aurora-v3.js`. The `filename` field in `hacs.json` remains `aurora-v3.js` while that filename is retained.

## Troubleshooting

- “Custom element doesn't exist”: check the loaded JavaScript, resource URL, and `custom:luma-home-card` type, then fully reload the page.
- Missing images: for the manual installation described here, check `assets: /local/luma-home/btn/`, including the trailing slash, and confirm that the images exist in `www/luma-home/btn/`.
- Greyed-out lights: check the entity ID and its availability in Home Assistant.
- Zero costs: set the rate and check the energy-consumption sensors.
- Wrong language: check `language: fr`, `language: en`, or `language: it`, and the JavaScript version actually loaded.
- Old text after updating: increase the resource's `?v=` parameter and reload the browser.

## Uninstalling

Delete the relevant dashboard, its resource if nothing else uses it, and the `www/luma-home` folder if no other installation uses it.

These steps do not automatically clear browser preferences or remove energy sensors configured separately.

For HACS installations, use the appropriate removal procedure and confirm that no other dashboard still requires the files.

## Status and limitations

The maintainer has confirmed operation of a tested version in Home Assistant and visually checked the French and English interface. Not every rare message or interaction has necessarily been validated.

The automated checks cover HACS requirements, JavaScript syntax, and equality of the reference and distribution files at the revisions checked. They do not replace functional testing of the final installation.

Changes to resource URLs, installation paths, or card identifiers require a new functional test.

The original README states that Aurora Glass v3 was tested by its author on Home Assistant 2026.9. This does not certify the derivative version.

To report an issue with this adaptation, open an issue in the repository distributing this version, including the language, loaded version, and reproduction steps.

## License and attribution

The derivative software is distributed under the [GNU GPL version 3](LICENSE).

You may use, study, modify, and redistribute the software, including commercially, subject to the license conditions. Distributed derivatives must, among other requirements, preserve applicable notices, identify modifications and their dates, and meet the licensing and Corresponding Source obligations.

Original notice preserved: © 2026 DomotikPro.it (Luca Pinelli).

Fonkyup's contributions do not replace the original project's rights and credits. Any separate terms applying to third-party components remain applicable.

The name Aurora Glass and the DomotikPro.it brand are mentioned to identify the original project. No trademark rights or endorsement are claimed. The public name of this derivative is Luma Home.

The software is provided without warranty, to the extent stated in the license and permitted by applicable law. LICENSE contains the full terms; this section is only a summary.

Preserve the LICENSE text without modification. Project and contribution notices belong in the documentation and source files, not inside the GPL text.

---

Original project: [DomotikPro.it](https://domotikpro.it) — Luca Pinelli.

Unofficial multilingual adaptation: Fonkyup.
