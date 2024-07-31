# Talon German
German Dictation Mode for the beta version subscription of Talon Voice.

This is a fork of earlier setups, adding some improvements.

This version uses that german conformer model instead of vosk. This results in two major benefits: (1) You can add unknown words (2) you no longer have to worry about misrecognitions with commands, since the conformer speech engine knows about the currently defined commands. Basically it now behaves like you got used to from the english speech models.

## Usage
Say `german [mode]` to switch from command mode to German dictation mode and `english` / `ego` to switch back.
Use `nimitz <german phrase>` for single german phrases like you would use `say <english phrase>` (from russian "nemetz" for "german").
Check out the _german.talon_ (and _german.py_) files for German commands.

## Improvements:
I added various improvements for myself. Check out _german.talon_ for more existing commands.

### Text editing and navigation
A handful of additional commands that make on-the-fly edits of text much more convenient.
especially:
* `springe links / rechts` will jump whole words in left / right direction
* `lösche links / rechts` will delete whole words in left / right direction
* `entferne links / rechts` will delete single chars in left / right direction
* `großgeschrieben` / `mach groß` helps fixing capitalization mistakes from vos
You can suffix most of these with a number to repeat them, for example `springe links 5`.

In addition to already existing `gehe rauf / runter / recht / links` for single char movements.

### Symbols
Some improvements regarding symbols - you can use more symbols and direct dictation now.
Also added more symbols I frequently used, for example `in Klammern` (` ()`), `Spiegelstrich` (` - `), `Ellipse` (`...`), `Schrägstrich oder` (` / `), `Zeilenumbruch`, `Leerzeichen` ...

### German mode / quick german phrases
The original setup introduced a way to dictate a quick german phrase while in english mode without having to switch to german mode and back (like a german `say` command).
This was originally just an improved version of the `german [mode]` command used to change modes (for example `german Hallo Welt` instead of `german <pause> Hallo Welt english <pause>`).
Note that the implementation for this is somewhat of hack and behavior might change with updates in talon or the english speech model.

Since I would sometimes switch into german mode when I did not want to or fail to remain in german mode (resulting in my german text getting interpreted as a bunch of english commands), I set up the quick german phrase and the german mode change to use separate commands (there is also the fact that my german accent made the 'r' in 'german' a bit harder to recognize when quickly chaining):
* `german` switches to german mode and stays there.
* `nimitz` (from russian "nemetz" for german) will interpret the following phrase as german and allow you to continue in english as before. This is the german equivalent of `say <english phrase>`.

Use `english`, or short `ego` (japanese "eigo" for english) to switch back.

### Quick access to configuration
Similar to `customize ...` in the community command set, following commands allow quick access to important configuration files:
* `[modifiziere | bearbeite] deutsche Wörter` opens a *additional_words_de.csv* file placed next to community *additional_words.csv*. Use this to add new words or fix misrecognitions as well as capitalisation mistakes coming from vosk. Note: actually, it works more like words_to_replace.csv, since it only replaces things that vosk recognized but cannot get it to recognize new stuff - I should rename that.
* `[modifiziere | bearbeite] deutsche Befehle` opens *german.talon*
The commands open a gvim instance.
Currently, the commands use a simple hard-coded path, so you will have to change that.


### Context sensitive dictation
Same as community, use the setting `user.context_sensitive_dictation` to activate / deactivate.
Uses the implementation from community, so you should get the same functionality.

Context sensitive dictation also applies to `nimitz <phrase>`, which means it is not necessary to add or remove spaces before inserting a german phrase (I find this to be very convenient).

### Eye tracker control
You can control your eye tracker with the commands `Tracking (an | aus | Augen | Kopf | kalibrieren)`.

## Caveats:
* Only primitive capitalization
* Punctuation is less smart than in community as well, especially if you do not use context sensitive dictation
* Trying to do `go to sleep` / `talon sleep` while in german mode will have no effect currently. You will have to cycle through sleep / wake however when switching back to english afterwards. Therefore, for sleep you have to switch back to an english mode beforehand, or mute the microphone.

## Todo:
* [ ] Rename additional_words_de.csv to words_to_replace_de.csv since that is what the file actually does
* [ ] Currently uses absolute paths for csvs, use relative paths (perhaps switch to .talon-list)
* [ ] Extract commonly used command prefixes like `springe`, `bearbeite deutsche`, `lösche`, `entferne` into something like a variable to make addition of alternate variations simpler and improve readability
* [ ] Better structure of commands, split into seperate files
* [ ] Add version of the `großgeschrieben` command that will permanently add the capitalized word to the csv
* [ ] Support for sleeping / waking while in german mode
* [ ] Remove custom *Clipscanner* clipboard implementation in favor of talon / community clipboard API

## Dependencies
This is a plug-in for Talon Voice (https://talonvoice.com/).
Requires the [talon beta](https://www.patreon.com/lunixbochs) subscription for its support of additional speech engines.
Assumes the [community command set](https://github.com/talonhub/community) to be present in the talon user directory.

## Setup
* Clone this repository into your talon user folder (`~/.talon/user`)
* Download the german conformer engine from talons context menu

## Related
Other related projects and repositories:
* [hanueles german port of knausj (the community command set)](https://github.com/hanuele/knausj_german) aims to offer a complete set of german commands mirroring knausj (not only limited to a dictation mode). Like this repo, requires knausj (community) being present in the talon user directory. Seems to be less maintained though at the moment.

Also visit the [#language-deutsch](https://talonvoice.slack.com/archives/CURG8FXAQ) channel in the talon slack in case you have any questions or problems.

