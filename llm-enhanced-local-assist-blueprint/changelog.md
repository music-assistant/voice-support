![Image](https://github.com/music-assistant/voice-support/blob/main/assets/music-assistant.png?raw=true)

# Changelog: Option 2 - LLM Enhanced automation

## 20250129

* fix: correct assistant typo throughout

## 20250128

* Initial version when the changelog was created

## 20250404

* Added logic to handle requesting to shuffle music

## 20250511
* Added fixes to ensure llm result is wrapped in action_data appropriately


## 20261116

* Use `entity_name(fallback=true)` instead of the `friendly_name` attribute for player names, as `friendly_name` is being deprecated since the naming changes in Home Assistant 2026.11. The minimum Home Assistant version is now 2026.11
