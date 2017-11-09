# Game Engines Filetypes Reverse Engineering

A work-in-progress repository containing templating and reading scripts along with file examples of different filetypes used within game engines.

##

### Contents:

* [Engines](#engines)
* [Filetypes](#filetypes)
* [Templates code-style](#templates-code-style)
* [Directory structure](#directory-structure)

##

### Engines

List of engines (or companies if engine name is unknown) which files are to be explored.

* [Gameloft](#gameloft-engine)
* ...

##

### Filetypes

List of filetypes which are either already known, at parsing stage or planned to get parsed.

Status legend:

* ![#00FF00](https://placehold.it/15/00FF00/?text=+) Known type
* ![#FFBB00](https://placehold.it/15/FFBB00/?text=+) File can be parsed but some fields are unknown
* ![#FFFF00](https://placehold.it/15/FFFF00/?text=+) Parsing in-progress
* ![#FF0000](https://placehold.it/15/FF0000/?text=+) Filetype is planned for future

#### Gameloft Engine

<table>
  <tr>
    <th>Extension</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .bar</td>
    <td></td>
  </tr>
  <tr>
  <td><img src="https://placehold.it/15/FFFF00/?text=+" /> <span class="">.bdae</span></td>
  <td>3D model including mesh, materials, textures, nodes, bones, SFX, animations.<br><i>Different games or game versions can use different file version.</i></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .beff</td>
    <td>Visual effects that can be attached to .bdae nodes.</td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .bin</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .dat</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .ikp</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FFBB00/?text=+" /> .itm</td>
    <td>Contains data about different .bdae models placed on a terrain chunk. Implicitly bound with .trn by game world position.</td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .msk</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .phy</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .riff</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .shw</td>
    <td></td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FFFF00/?text=+" /> .trn</td>
    <td>Represents a terrain chunk of 64x64 size. Known info: heightmaps.</td>
  </tr>
  <tr>
    <td><img src="https://placehold.it/15/FF0000/?text=+" /> .wld</td>
    <td></td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
  </tr>
</table>

##

### Templates code-style

Extension templates are mainly written using [010 Editor](https://www.sweetscape.com/010editor/) (any other templating application is OK as long as it allows making file-parsing scripts). While using it, a good way is to visualize parsed parts of a file even if particular byte sequence meaning is unknown  to you. You should also stick to this styling even if you can parse every byte of a certain extension since there can be one file with extra information which is not handled by your template.

Color scheme used by me (and proposed for usage by any contributor) is similar to status legend at [Filetypes](#filetypes) section:

- ![](https://placehold.it/15/00FF00/?text=+) `0x00FF00` - known meaning of byte sequence;
- ![](https://placehold.it/15/FFFF00/?text=+) `0x00FFFF` - byte sequence usage is known but meaning is not (for example, 4-byte value can be an offset to unknown region);
- ![](https://placehold.it/15/00BBFF/?text=+) `0xFFBB00 `- byte sequence contains a constant *zero* value across multiple file examples and has unknown meaning;
- ![](https://placehold.it/15/FF8800/?text=+) `0x0088FF` - byte sequence contains a constant *non-zero* value across multiple file examples and has unknown meaning;
- ![](https://placehold.it/15/FF0000/?text=+) `0x0000FF` - unknown meaning of byte sequence.

Keep in mind, that [010 Editor](https://www.sweetscape.com/010editor/) colors are written like BGR, not RGB.

##

### Directory structure

A well-structured storage is easy to search to maintain! That's why a certain logic should be used. In our case, we can have multiple game engines use same extension but those files be of different types.

A top-level directory `engines` is used to contain game engines folders. Navigating to certain engine will show a list of folders with extensions supplied as folder names. In case a filetype can be of multiple versions, every version (prefixed with `v`) is contained as a separate folder. Inside extension folder (or its version) there must be `samples`, `scripts` and `templates` folders.


Example structure:

```
engines/
├── Gameloft/
│   ├── bdae/
│   │   ├── v0.0.0.779/
│   │   │   ├── samples
│   │   │   │   └── elf_low_h.bdae
│   │   │   ├── scripts
│   │   │   │   └── bdae_import.cs
│   │   │   └── templates
│   │   │   │   └── BDAE.bt
│   │   └── v0.0.0.946/
│   │       ├── samples
│   │       ├── scripts
│   │       └── templates
│   │           └── BDAE.bt
│   └── trn/
│       ├── samples
│       ├── scripts
│       └── templates
│           └── TRN.bt
├── Frostbite/
└── General/
```
