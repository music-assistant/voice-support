![Image](https://github.com/music-assistant/voice-support/blob/main/assets/music-assistant.png?raw=true)

# Changelog: Option 1 - Fully local automation

## 20250128

* Initial version when the changelog was created

## 20250404

* Added logic to handle requesting to shuffle music

## 20261116

* Added version 2 (`mass_assist_blueprint_v2_en.yaml`, English only for now). See the README for the differences with version 1
* Version 1 is unchanged

* Use `entity_name(fallback=true)` instead of the `friendly_name` attribute for player names, as `friendly_name` is being deprecated since the naming changes in Home Assistant 2026.11. The minimum Home Assistant version of version 2 is now 2026.11
