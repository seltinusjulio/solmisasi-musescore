# Solmisasi MuseScore Plugin

A MuseScore plugin that displays Indonesian numerical notation (solmisasi/not angka) above staff notation. This plugin is a modified version of the Note Names plugin, specifically designed for Indonesian music notation.

## Features

- Displays numerical notation (solmisasi/not angka) above staff notes
- Supports multiple octaves with dot notation:
  - Standard octave (C4-B4): No dots
  - Higher octave (C5-B5): Single dot above note
  - Lower octave (C3-B3): Single dot below note
  - Two octaves higher (C6-B6): Double dots above note
  - Two octaves lower (C2-B2): Double dots below note
- Handles grace notes with smaller font size
- Works with chord notation
- Supports both selected passages and full score processing

## Requirements

- MuseScore 3.x or 4.x
- Download **Parnumation** font (recommended for optimal display)
  - Parnumation 3.0 (original, created by Rikardo Lumbantobing):
  - Download from: https://gnibot.blogspot.com/2014/07/parnumation-3.html  
  - Parnumation 3.1 (modified to display short lines _ above single quarter notes)
  - Available in this repo: https://github.com/seltinusjulio/solmisasi-musescore/
  - Install the font on your system for the best visual results

## Installation

1. Download the plugin file (`solmisasi.qml`)
2. Place it in your MuseScore plugins folder:
   - **Windows**: `%USERPROFILE%\Documents\MuseScore3\Plugins` (or `MuseScore4\Plugins`)
   - **macOS**: `~/Documents/MuseScore3/Plugins` (or `MuseScore4/Plugins`)
   - **Linux**: `~/Documents/MuseScore3/Plugins` (or `MuseScore4/Plugins`)
3. Restart MuseScore
4. Enable the plugin in **Plugins → Plugin Manager**

## Usage

1. Open your score in MuseScore
2. Set Staff text to use Parnumation font (Format > Style > Text styles > Staff)
3. Select the passage you want to add solmisasi notation to (or leave unselected for entire score)
4. Go to **Plugins → Composing/arranging tools → Solmisasi**
5. The plugin will add Solmisasi numerical notation above your staff notes

## About Solmisasi

Solmisasi (also known as "not angka" or numerical notation) is a popular music notation system in Indonesia where:
- Do = 1
- Re = 2
- Mi = 3
- Fa = 4
- Sol = 5
- La = 6
- Ti = 7

This system is widely used in Indonesian music education and traditional music.


## About Parnumation

**Parnumation** (short for "Pargodungan Numbered Notation") is a custom font created by **Rikardo Ladesman Lumban Tobing** in 2014 using [Fontographer](https://www.fontlab.com/font-editor/fontographer/) and [High-Logic FontCreator](https://www.high-logic.com/font-editor/fontcreator). This font transforms regular text input into numbered notation, making it particularly useful for writing music scores in word processors such as Microsoft Word. Writing music with this font has become a popular method for creating clean and easy-to-produce numbered notation scores. Previously, I made minor modifications to create **Parnumation 3.1**, which introduced single-line markings for half notes (as opposed to the extended line markings used for double notes in Parnumation 3.0). For more details about the Parnumation font, you can visit Rikardo's blog [here](https://gnibot.blogspot.com/2014/07/parnumation-3.html).

## Technical Details

- **Plugin Version**: 1.0
- **Compatibility**: MuseScore 3.x and 4.x
- **Font Size**: Grace notes are displayed at 70% of normal font size
- **Placement**: Notes in voices 1 and 3 are placed below the staff, others above

## Octave Mapping

The plugin uses MIDI pitch values to determine octave prefixes:
- C2 (MIDI 36-47): "8" prefix > double dot under note
- C3 (MIDI 48-59): "s" prefix > single dot under note
- C4 (MIDI 60-71): No prefix (standard octave)
- C5 (MIDI 72-83): "a" prefix > single dot above note
- C6 (MIDI 84-95): "9" prefix > double dot above note
- Other octaves: "?" prefix

**Note**: The visual representation of dots above/below notes requires the Parnumation font for proper display. Without this font, the prefixes will appear as regular text characters.

## Credits

- **Original Note Names Plugin**: Werner Schweer, Joachim Schmitz, Jörn Eichler, Johan Temmerman
- **Solmisasi Modification**: Angelo Seltinus, OFMCap / Seltinus Julio (2025)
- **Parnumation Font**: Created by Rikardo Ladesman Lumban Tobing

## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License version 2 as published by the Free Software Foundation.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to improve the plugin.

## Links

- [GitHub Repository](https://github.com/seltinusjulio/solmisasi-musescore)
- [Parnumation Font](https://gnibot.blogspot.com/2014/07/parnumation-3.html)
- [MuseScore Official Website](https://musescore.org)