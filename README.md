# Voice support tools and scripts for Music Assistant

Bridge the gap between Home Assistant Assist and Music Assistant for voice-initiated music control.

This repository is meant to be an effort to collect scripts, blueprints, HOWto's etc. and their translations to enable full Voice control of music playback.
Home Assistant itself has very limited intents for music/media control, and especially there is no support for initiating playback of music by voice.
While this support is on the horizon to be added, there is still a lot to investigate about that to create a universal way to provide that support in HA natively. Maybe the resources/experiments from this repository can help make that journey easier in the future.

**Community driven effort!**
Please reach out if you want to help out or have great ideas!
If you have something to share here, feel free to PR it or ask to be added to the maintainers.

## Option 1: Local Assistant Blueprint

Blueprint to initiate media playback using pure local intent handling (custom sentences) so no Cloud-LLM involved.
This however means that requests need to be very carefuly formulated.

The Blueprint is located in the `local-assist-blueprint` folder of this repository and can be imported by using the following buttons:

|Language|Import button|
|---|---|
|Dutch|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_nl.yaml)|
|English|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_en.yaml)|
|German|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_de.yaml)|
|Brazilian Portuguese|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_pt-br.yaml)|
|Spanish|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_es.yaml)|
|Italian|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_it.yaml)|
|Slovak|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_sk.yaml)|
|Hungarian|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Flocal-assist-blueprint%2Fmass_assist_blueprint_hu.yaml)|

In case your language is not listed above, you provide tranlsations yourself in the blueprint settings.


### Blueprint setup

#### Required 

* Set a `Default Player` to be used when no target is mentioned in the request and
the request doesn't come from an area with a Music Assistant player.

#### Optional

* Change the trigger sentence or add more, you can also use this to translate 
the sentence to your own language.

* Change the responses or translate them to your own language.


### Usage
*see the translated blueprints for translated usage*

All sentences must:

* start with the words `Shuffle`, `Play` or `Listen to` followed by the item type `artist`/`track`/`album`/`playlist`/`radio` and then the name of the item
* if starting with `Shuffle`, the player that handles the request will have it's shuffle setting turned on, otherwise it will be turned off
* for album and track be optionally followed by `by [the] artist` and then the artist name
* then be optionally followed by an area name or device name
* then, for artist, track, album or playlist, be optionally followed by the phrase `using radio mode`

#### Accepted variations

usage of the article `the` is optional

|Media type|Accepted variations|
|---|---|
|`artist`|`band`, `group`|
|`track`|`song`|
|`radio`|`radio station`, `radio`|
|`playlist`||


#### Examples

```
Play the artist Pink Floyd in the kitchen
Listen to album Jagged Little Pill in the study
Listen to the album Greatest Hits by the artist James Taylor in the kitchen
Play track New Years Day in the bedroom
Play track New Years Day in the bedroom using radio mode
Play the song A Hard Days Night by Billy Joel in the bedroom
Listen to the playlist Classic Rock in the study
Listen to the radio station BBC Radio 1 in the bedroom
Play the album Classical Nights on the Bedroom Sonos Speaker
Listen to the record Classical Nights on the Bedroom Sonos Speaker
Play the band U2
Shuffle songs by Muse.
Shuffle the album Classical Nights on the Bedroom Sonos Speaker
```

## Option 2 Local Assist enhanced by an LLM integration like [Open AI Conversation](https://www.home-assistant.io/integrations/openai_conversation/) (ChatGPT) or [Google Generative AI](https://www.home-assistant.io/integrations/google_generative_ai_conversation/) (Gemini).

The groundwork for this option was done by [JLo](<https://github.com/jlpouffier>) in his [blog post](<https://blog.jlpouffier.fr/chatgpt-powered-music-search-engine-on-a-local-voice-assistant/>) on GPT-powered music search. This blog post was a big inspiration for the LLM enhanced automation, and also enabled the full LLM script. So big thanks to JLo!

The blueprint is located in the `llm-enhanced-local-assist-blueprint` folder of this repository and can be imported by using the following button:


|Language|Import button|
|---|---|
|English|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-enhanced-local-assist-blueprint%2Fmass_llm_enhanced_assist_blueprint_en.yaml)|
|French|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-enhanced-local-assist-blueprint%2Fmass_llm_enhanced_assist_blueprint_fr.yaml)|
|Hungarian|[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-enhanced-local-assist-blueprint%2Fmass_llm_enhanced_assist_blueprint_hu.yaml)|

### Translations
|Language|Information|
|---|---|
|Dutch|[Information](/llm-enhanced-local-assist-blueprint/mass_llm_enchanced_assis_bluerpint_nl.md)|


### Configuration

1. An LLM integration needs to be set up. This can be an already existing integration. This automation is intended to be used with an LLM Conversation Agent which doesn't allow home control (No control selected instead of Assist). Usage with an LLM which has control over your entities can result in errors, like targeting a media player which isn't a Music Assistant player. If you want to use an existing LLM with home control enabled, [Option 3](#option-3-script-which-can-be-used-as-a-tool-by-an-llm-integration-like-open-ai-conversation-chatgpt-or-google-generative-ai-gemini) is the preferred option.
2. Import the Blueprint using the button above.
3. Create the automation using the blueprint. Choose the LLM agent from step 1. Optionally you can change settings for Music Assistant playback such as a default player, and whether to use Play Continously. You can also adjust the way voice responses are created as well as tweak the LLM Prompt as needed for your particular model. See the setting descriptions for more information.
4. Save the automation.


### Blueprint setup

#### Required 

* Select an LLM conversation agent to be used with the automation. The blueprint is 
intended to be used with an LLM conversation agent without control of the house.

#### Optional

* Set a `Default Player` to be used when no target is mentioned in the request and
the request doesn't come from an area with a Music Assistant player.
* Change the setting for `Radio Mode`. By default this is set to use the `Don't stop 
the music` setting on the Music Assistant player.
* Change the trigger sentence or add more, you can also use this to translate 
the sentence to your own language.
* Change the responses or translate them to your own language.
* Change the setting to expose area names and player names to the LLM, the default 
setting is to send them. In case you change the settings in the blueprint and 
do not expose the area names and player names to the LLM, the name must exactly 
match the name of the area or player in Home Assistant. So when the area name is 
_Bedroom Sophia_ it does not work if you you say _Sophia's Bedroom_ or when the 
Speech to Text conversion uses _Sofia_ instead of _Sophia_. Unfortunately aliases 
can't be used in the automation, as there is no template to get the aliases of areas 
or entities. Capitalization of words does't matter, so _bedroom sophia_ will still 
match if the area name in Home Assistant is _Bedroom Sophia_
* Change the prompt which is used to have the LLM provide the correct data. 
You don't need to translate this if you use a different language.


### Usage

All sentences must:

* start with the words `Shuffle`, `Play` or `Listen to` followed by a query about what you
want to play
* if starting with `Shuffle`, the player that handles the request will have it's shuffle setting turned on, otherwise it will be turned off
* then be optionally followed by one or more area names and/or one or more device
names to play the music on.

### How the target for the media is determined:

1. In case one or more areas and/or one or more Music Assistant players are mentioned 
in the request, these areas and/or players are used.
In case you don't expose the names, and the area or player mentioned doesn't match exactly 
with the area or player name in Home Assistant, Assist will use the `No target response`.
2. If no target was mentioned in the request, the automation will first check if the 
request came from a device in an area. If there is also a Music Assistant player 
in that same area, the music will be played there.
3.  If no target was mentioned in the request and the voice satellite area could also 
not be used, then the `Default Player` set in the blueprint will be used. In case no 
`Default Player` is set, the `No target response` will be returned.


#### Examples

```
Play the best songs from Pink Floyd in the kitchen
Listen Jagged Little Pill in the study
Listen to the album Greatest Hits by James Taylor in the kitchen
Play track New Years Day in the bedroom
Play A Hard Days Night by Billy Joel in the bedroom
Listen to the playlist Classic Rock in the study
Listen to BBC Radio 1 in the bedroom
Play the album Classical Nights on the Bedroom Sonos Speaker
Listen to the record Classical Nights on the Bedroom Sonos Speaker
Play songs by U2
Play music by the composer from oppenheimer
Play the album that has the nude baby swimming in the water on the cover
Shuffle songs by Muse.
Shuffle the album Classical Nights on the Bedroom Sonos Speaker
```

### Option 2 - version 2 (AI Task)

Version 2 is a rewrite which uses the [AI Task](https://www.home-assistant.io/integrations/ai_task/) action `ai_task.generate_data` with structured output instead of asking a conversation agent for JSON. It is added next to the original blueprint, because the inputs changed too much to update the original in place. The original blueprint keeps working.

The blueprint is located in the `llm-enhanced-local-assist-blueprint` folder of this repository and can be imported by using the following button:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-enhanced-local-assist-blueprint%2Fmass_llm_ai_task_assist_v2.yaml)

#### Requirements

* Home Assistant 2025.8 or newer
* An AI Task entity (for example from [Google Generative AI](https://www.home-assistant.io/integrations/google_generative_ai_conversation/), [OpenAI Conversation](https://www.home-assistant.io/integrations/openai_conversation/) or [Ollama](https://www.home-assistant.io/integrations/ollama/)). It doesn't need access to your house, the blueprint hands it everything it needs.

#### What is different compared to version 1

|Topic|Version 1|Version 2|
|---|---|---|
|LLM call|Conversation agent, the LLM has to answer in JSON which is parsed afterwards|`ai_task.generate_data` with a structure, the answer always has the right shape|
|Valid targets|The LLM answers with area and player names, which are matched against your Music Assistant areas and players with a text search|Media types, areas, floors and Music Assistant players are selectors, so the LLM can only return values which exist. The result is checked again in the automation|
|Prompt|Nine separate prompt inputs plus a combined prompt|One `Instructions for the AI` input, the output format is enforced by the structure|
|Area/player names|Two settings (`expose_players`, `expose_areas`). Names are matched on the exact name when not exposed|One setting `Share area, floor and player names with the AI`. When enabled the names are sent together with their ids, so renamed areas and old random area ids work. When disabled the AI only returns the location as spoken and the names are matched inside Home Assistant|
|Floors|Not supported|Supported ("play jazz downstairs")|
|Media check|Names are passed to Music Assistant as they are|Every item is looked up with `music_assistant.search` first. Assist answers with the real title and artist, and uses the `Not found response` when nothing matches. Matches are only accepted when the artist (or title) resembles the request, so a wrong item isn't played|
|Response speed|Assist waits until playback has started|Assist answers as soon as the media is found, playback is started by a second run of the automation|
|Several players in an area|All Music Assistant players in the area are used|Optionally only the players selected in `Preferred players per area`. Unavailable players are skipped|
|Queue|Always replaces the queue|`Queue behaviour` setting, which you can override by voice: "add ... to the queue", "play ... next", "play ... now and keep the queue"|
|Latest release|Depends on what the model knows|"play the latest album by ..." looks up the newest album in your library, so it also works when the model's knowledge is outdated. Only albums in your library are found this way, otherwise the title suggested by the AI is used|
|Playback control|"Play" sentences which only want to resume or skip are handled as a new request|The AI also classifies the request. Resume, next, previous, pause and stop are done on the players in the target area|
|Shuffle|Shuffle on/off per request|Same, but shuffle is not changed when you add to an existing queue|
|Responses|Area, player and area+player responses|Same, plus `Not found`, `Playback control` and `Error` responses. `shuffle` and `enqueue` are available as variables, `<media_info>` is replaced by the title that was found|

#### Removed and renamed inputs

|Version 1|Version 2|
|---|---|
|`llm_agent`|`ai_task_entity` (leave empty to use the preferred AI Task entity)|
|`expose_players`, `expose_areas`|`expose_names`|
|`llm_prompt_*`, `llm_prompt`|`llm_instructions`|
|`play_continuously`, `default_player`, responses, `trigger`, `combine_text`|Unchanged|
|-|New: `max_tracks`, `area_players`, `enqueue`, `verify_media`, `artist_text`, `not_found_response`, `control_response`, `error_response`|

#### Switching from version 1

Both versions listen to the same sentences, so create the new automation from the version 2 blueprint, check it with a few requests and then disable (or delete) the automation based on version 1. Your own prompt changes from version 1 can't be copied one to one, because the output format is no longer part of the prompt. Add what is specific for your setup to `Instructions for the AI`.

#### Examples

```
Play the latest album by Foo Fighters in the kitchen
Add Bohemian Rhapsody by Queen to the queue in the living room
Play the album that has the nude baby swimming in the water on the cover
Shuffle jazz downstairs
Continue playing in the bedroom
```

The `Usage` and `How the target for the media is determined` sections of option 2 above apply to version 2 as well.

## Option 3: Script which can be used as a tool by an LLM integration like [Open AI Conversation](https://www.home-assistant.io/integrations/openai_conversation/) (ChatGPT) or [Google Generative AI](https://www.home-assistant.io/integrations/google_generative_ai_conversation/) (Gemini).

The blueprint is located in the `llm-script-blueprint` folder of this repository and can be imported by using the following button:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-script-blueprint%2Fllm_voice_script.yaml)

The language of the voice command is not relevant, the script has all descriptions in English, but it will be used by voice commands issued in a different language as well.

### Configuration

1. An LLM integration needs to be set up, and used in your Voice pipeline
2. Allow the LLM integration to access your house, otherwise it won't be able to use the script as a tool
3. Import the Blueprint using the button above
4. Create a script using the blueprint, optionally you can adjust the prompt settings which are the basis on how the script will be used by the LLM
5. Optionally add additional actions to be performed after the Music Assistant play media step while setting up the script
5. Save the script, make sure to give it a clear description, as that is what will be used by the LLM to determine when to use it (see example below). 
6. Expose the script to Assist

Suggestion for the script description:
>   This script is used to play music based on a voice request. The tool takes the following arguments: media_type, artist, album, media_id, radio_mode, area. media_id and media_type are always required and must always be supplied as arguments to this tool. An area or Music Assistant media player can optionally be provided in the voice request as well. Use the parameters as described in the description of each parameter. Use this tool whenever the user requests to play music.

### Usage

There is no required format for the sentences, just use anything you can imagine to play music. You can add an area in which it should be played or a Music assistant player. If the area and Music Assstant player are both ommited from your voice request, it will take the area from which the command is issued. If the area can not be determined (for example if you issued a command from the browser), it will use the default player in case you provided one. If no default player is provided, it will ask to specify an area or player.

It will differ per LLM integration how well the commands are understood. If the command is not clear enough, the LLM might ask for more details. Escpecially for smaller models more guidance can be required. If needed you can adjust the prompts used for each parameter.

### Examples
All responses and results are generated each time the script is used, so don't expect the exact same results as below.

- Command: *Play the album from that grunge band with the baby swimmng towards a bank note on the album cover in the room in which we prepare our meals*
  
  Response:  *The album "Nevermind" by Nirvana is now playing in the area in which meals are prepared*
  
  Result: The album "Nevermind" will be played in the kitchen

- Command: *Play some classic rock songs*
  
  Response: *I've started playing some classic rock songs in the office. Enjoy the music!*

  Result: The following 5 songs are played
    * Led Zeppelin - Stairway to Heaven
    * Queen - Bohemian Rhapsody
    * The Rolling Stones - Paint It Black
    * The Who - My Generation
    * AC/DC - Back in Black

- Command: *Shuffle some music by Billy Talent*

  Response: *I am now shuffling music by Billy Talent in the workshop. Enjoy the tunes!*
  
  Result: songs by Billy Talent will be played in the area the command was issued from, and the player in that area will have its shuffle setting turned on
