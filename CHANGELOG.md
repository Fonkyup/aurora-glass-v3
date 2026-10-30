# Changelog

## Unreleased

### Added
- French and English interface translations.
- French and English installation-guide translations.
- Multilingual project-origin and licensing notices.
- **Configurable zones**: display a custom per-zone layout with lights (`lights`), motion sensors (`motions`), doors/windows (`doors`), locks (`locks`), and individual climate devices (`climates`).
- **Zone climate control**: per-zone climate panel for thermostats with +/- adjustment, mode selection, and heating-only heater display.
- Garage heater image support for warming panel as available (use image library with `climate_` prefix or manual mapping).
- **Automated tests**: bench tester for card rendering, sensor/device mapping, and zone layout variations.

### Changed
- Public project name changed to Luma Home.
- Card registration and installation paths updated for Luma Home.
- Licensing explanations clarified in the documentation.
- README updated to describe both historic mode (overrides via `entities`) and new zone mode (`zones` list of per-room configurations).

### Preserved
- Original credits and copyright notices.
- GNU GPL version 3 license.
- Original Italian interface.