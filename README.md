# Luma Home — Multilingual dashboard for Home Assistant

[English](README.md) | [Français](README.fr.md) | [Italiano](README.it.md)

An unofficial derivative of Aurora Glass v3, adapted by Fonkyup with a French, English, and Italian interface.

> Renaming status: Luma Home is the public name used in this documentation. The instructions below retain the current technical names (`aurora-v3.js`, `custom:aurora-v3-card`, and the existing folders). Do not replace them with `luma-home.js` or `custom:luma-home-card` until the code and distributed files have been migrated together.

![Interface inherited from Aurora Glass v3, the original project](docs/dashboard-casa-notte-intera.webp)

A custom card that turns a Home Assistant dashboard into a living scene: the sky, sun, moon, and the windows of the little house follow the real time of day. Ten animated worlds, eleven weather effects, buttons made from images and GIFs, an alarm, climate control, cameras, and an Energy view calculating costs from your own rate.

## Origin and contributions

This version is based on Aurora Glass v3, created by DomotikPro.it (Luca Pinelli).

Original notice preserved: © 2026 DomotikPro.it (Luca Pinelli).

Adaptation and translations: Fonkyup.

Work completed through October 25, 2026:
- added French and English interface translations;
- adapted interface text and dynamic messages;
- translated the installation guide into French and English;
- added this documentation and clarified the origin of the derivative version.

The original Italian language is retained. This version is not an official release and is not presented as endorsed by DomotikPro.it or Luca Pinelli.

The screenshots below come from the original project; they do not demonstrate validation of every translation.

| Tablet | Energy | Mobile |
|---|---|---|
| ![Tablet](docs/tablet-casa-tramonto.webp) | ![Energy](docs/energia-vista.webp) | ![Mobile](docs/mobile-casa-notte-sm.webp) |

## Original project resources

These links refer to Aurora Glass v3, not necessarily to the translated version:
- Original live demo, in Italian: https://domotikpro.it/aurora-glass-v3-demo/index.html
- Original illustrated guide, in Italian: https://domotikpro.it/progetti/aurora-glass-v3
- Original author's videos, in Italian: https://www.youtube.com/@domotikproit
- Original repository: https://github.com/lucalux00/aurora-glass-v3

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

## Installing this version

The paths below match the current file layout, before any technical renaming.

The original guide is [LEGGIMI.txt](aurora-glass-v3/LEGGIMI.txt). YAML example comments may still be in Italian.

### About HACS

The original project's HACS instructions use `lucalux00/aurora-glass-v3`: this installs the original version, not this adaptation.

A HACS installation procedure for this derivative still needs validation. Until then, use the manual installation below and the files from the branch containing the translations.

### 1. Copy the files

Copy the `aurora-glass-v3/www/aurora-v3` folder into the `www` folder of your Home Assistant configuration using File editor, Samba, or Studio Code Server.

The result should be:

```text
www/aurora-v3/aurora-v3.js
www/aurora-v3/btn/…
```

If you have just created `www`, restart Home Assistant once.

Open `<Home Assistant address>/local/aurora-v3/aurora-v3.js` in your browser: JavaScript text should appear.

### 2. Add the resource

Enable Advanced mode in your profile.

Settings → Dashboards → menu ⋮ → Resources → Add resource:
- URL: `/local/aurora-v3/aurora-v3.js?v=1`
- Type: JavaScript module.

Increase the number after `?v=` when updating. If an older installation exists, check the resources before adding another one to avoid loading two versions of the same card.

### 3. Create the dashboard

Settings → Dashboards → Add dashboard → New dashboard from scratch.

Suggested title: `Luma Home`.

### 4. Paste the configuration

Open the dashboard → pencil → menu ⋮ → Raw configuration editor.

On a new dashboard, paste the contents of [Dashboard example](luma-home/dashboard-example.en.yaml) and save. Back up the configuration before replacing an existing dashboard's contents.

Lights remain greyed out until you configure your own entities.

### 5. Choose the language and map your entities

Keep your other card options and add the language at the same level as `type` and `assets`:

```yaml
type: custom:aurora-v3-card
assets: /local/aurora-v3/btn/
language: en
```

Supported values: `fr` for French, `en` for English, and `it` for Italian. Without a language option, the current code defaults to Italian.

Developer tools → States: find your entity IDs and configure `entities:` as shown in [Card options](luma-home/card-example.en.yaml).

### 6. Configure energy — optional

Set your power sensor, in watts, in `energy.power`.

For energy-consumption meters in kWh, see [Energy meters](luma-home/aurora-energia.en.yaml).

In the Energy view, open the rate settings and enter your price per kWh. Displayed costs are estimates calculated from the configured consumption readings and rate.

## Troubleshooting

- “Custom element doesn't exist”: check the resource URL and `custom:aurora-v3-card` type, then fully reload the page.
- Missing images: check that `assets` is `/local/aurora-v3/btn/`, including the trailing slash.
- Greyed-out lights: check the entity ID and its availability in Home Assistant.
- Zero costs: set the rate and check the energy-consumption sensors.
- Wrong language: check `language: fr`, `language: en`, or `language: it`, and the JavaScript version actually loaded.
- Old text after updating: increase the resource's `?v=` parameter and reload the browser.

## Uninstalling

Delete the relevant dashboard, its resource if nothing else uses it, and the `www/aurora-v3` folder if no other installation uses it.

This does not describe clearing preferences stored in your browser or removing energy sensors added separately.

## Status and limitations

The French and English interface has been visually checked by the maintainer. Not every rare message or interaction has necessarily been validated.

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
