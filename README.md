# games_translation

Translations of games supported by ScummVM.

## MACS2 – Schatz im Silbersee

English translation for *MACS2 – Schatz im Silbersee*

- `en.po` - full-game English translation
- `macs2.pot` - translation template extracted from the game data

### Building `macs2_translation.dat`

ScummVM loads a binary translation file named `macs2_translation.dat` from the game directory. Build it from `en.po` with the `create_macs2_translation` tool from [scummvm-tools](https://github.com/scummvm/scummvm-tools):

```bash
./create_macs2_translation pack en.po macs2_translation.dat
```

Copy the resulting file into your game folder (alongside `RESOURCE.MCS`).

### Extracting a new template

To regenerate the `.pot` template from the original game data:

```bash
./create_macs2_translation extract /path/to/Schatz_im_Silbersee/RESOURCE.MCS macs2.pot
```

### PO format notes

Each entry uses a context id and line breaks that must match the German original:

```
msgctxt "scene:2:0"
msgid ""
"Eine schmucke Wand-\n"
"lampe."
msgstr ""
"A handsome wall-\n"
"lamp."
```

- `scene:N:I` - scene dialogue and descriptions
- `object:N:I` - object interaction text
- `hotspotlabel` / `objectlabel` - on-screen overlay names

Keep the same number of lines and `\n` breaks as the German `msgid`; the engine displays each line separately with a fixed width.
