# games_translation

Translations of games supported by ScummVM.

## MACS2 – Schatz im Silbersee

English and Swedish translations for *Der Schatz im Silbersee* (ScummVM engine: MACS2, game ID: `sis`).

- `en.po` - English translation shared by the full DOS game and DOS demo
- `sv.po` - Swedish translation shared by the full DOS game and DOS demo
- `macs2.pot` - translation template extracted from the game data

### Building translation packages

ScummVM loads optional `sis-translation-<lang>.dat` packages from the game directory. Use the language code from the PO filename, such as `en` for English or `sv` for Swedish. Build each package with the `create_macs2_translation` tool from [scummvm-tools](https://github.com/scummvm/scummvm-tools):

```bash
./create_macs2_translation pack en.po sis-translation-en.dat
./create_macs2_translation pack sv.po sis-translation-sv.dat
```

Copy both files into the full DOS game or DOS demo folder alongside `RESOURCE.MCS`. The same packages work with both releases. Multiple languages can be installed together. In ScummVM, select the game, open **Game Options**, and choose **English** or **Swedish** under **Translation** on the **Game** tab. Choose **Original** to play in German. The choice is saved per game target.

Translations do not create separate detected game variants: the original German DOS game is detected as `sis-de` and the DOS demo as `sis-demo-de`, regardless of which packages are installed. Translation packages are installed separately and are not embedded in or bundled with ScummVM. The old `macs2_translation.dat` filename is no longer loaded.

The engine maps the DOS demo's different object IDs and scene string indices to the full-game PO entries. The demo-only chapter-end message retains its German text because it has no full-game translation entry. The Amiga demo is not supported by these packages.

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
- `uilabel` - action-bar and HUD text; preserve `%s` / `%d` placeholders

Keep the same number of lines and `\n` breaks as the German `msgid`; the engine displays each line separately with a fixed width. Soft hyphens used to pad unused translated lines are hidden while preserving blank lines. An empty DAT entry still falls back to the German original.
