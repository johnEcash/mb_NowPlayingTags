# mb_NowPlayingTags

A [MusicBee](https://www.getmusicbee.com/) plugin that writes information about the currently playing track to a plain text file every second, and optionally exports the cover art to an image file. Both files can be read by any external program or overlay tool (e.g. a streaming overlay, a Stream Deck plugin, or a custom display).

---

## Features

- Writes track metadata to a plain text file every second
- Immediately updates the file when the track changes or playback starts, pauses or stops
- Exports cover art to an image file (JPEG, PNG, BMP or GIF)
- Automatically converts cover art to the format matching your chosen file extension
- Reports shuffle, Auto DJ and repeat state
- Configurable output paths via a settings dialog inside MusicBee
---

## Output

### Text file

The text file (`NowPlaying.txt` by default) contains one key=value pair per line:

```
artist=Daft Punk
title=Something About Us
album=Discovery
love=1
duration=4:38
position=1:22
shuffle=0
autodj=0
repeat=none
```

| Key | Description |
|---|---|
| `artist` | Artist name |
| `title` | Track title |
| `album` | Album name |
| `love` | `1` = loved, `-1` = banned, `0` = neither |
| `duration` | Total track length (`m:ss` or `h:mm:ss`) |
| `position` | Current playback position (`m:ss` or `h:mm:ss`) |
| `shuffle` | `1` = on, `0` = off |
| `autodj` | `1` = on, `0` = off |
| `repeat` | `none`, `all` or `one` |

When nothing is playing, all track fields (`artist`, `title`, `album`, `love`, `duration`, `position`) are empty. Shuffle, Auto DJ and repeat always reflect the current player state.

The file is encoded in **UTF-8 without BOM** and uses Windows line endings (`\r\n`).

### Cover art file

The cover art file (`cover.jpg` by default) contains the album art of the currently playing track. When the track changes, the file is replaced. When playback stops, the file is deleted.

The image is saved in the format matching the extension you choose (`.jpg`, `.png`, `.bmp` or `.gif`). If the source art is in a different format it is converted automatically. Transparent backgrounds are filled with white when converting to JPEG.

---

## Requirements

### To use the plugin

- [MusicBee](https://www.getmusicbee.com/) 3.x or later (Windows)

## Installation

1. Close MusicBee completely.
2. Copy `mb_NowPlayingTags.dll` to the MusicBee Plugins folder:
   - Standard install: `C:\Program Files (x86)\MusicBee\Plugins\`
   - Microsoft Store install: `%AppData%\MusicBee\Plugins\`
3. Start MusicBee.
4. Go to **Edit → Preferences → Plugins** and make sure **Now Playing Tags** is enabled.

> After updating the plugin, always close MusicBee first before replacing the DLL, as MusicBee keeps the file locked while running.

---

## Configuration

1. Open **Edit → Preferences → Plugins**.
2. Select **Now Playing Tags** and click **Configure...**.
3. The settings dialog has two fields:

   | Field | Description |
   |---|---|
   | **Text file** | Full path to the output text file, e.g. `C:\Stream\NowPlaying.txt` |
   | **Cover image** | Full path to the cover art image, e.g. `C:\Stream\cover.jpg`. Leave empty to disable cover art export. |

4. Use **Browse...** to pick a location, or type the path directly.
5. Click **OK** to save. The new paths take effect immediately — no restart needed.

### Default paths

If you have not configured any paths, the plugin uses:

| File | Default location |
|---|---|
| Text file | `%AppData%\MusicBee\NowPlaying.txt` |
| Cover image | `%AppData%\MusicBee\cover.jpg` |

Settings are stored in `%AppData%\MusicBee\mb_NowPlayingTags.settings.txt`.


