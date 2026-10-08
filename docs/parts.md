title:Reusable Parts in the Example Decks

Reusable Parts in the Example Decks
===================================
A catalog of the reusable _contraptions_ (instances of Prototypes) and _modules_ that ship inside the decks in `examples/decks`. Descriptions come from each part's own `description:` field; function names were read from the module scripts. Nothing here is a built-in of Decker itself: to use a part, copy it into your deck with the Font/Deck Accessory Mover (see [Resources](decker.html#resources) and [Modules](decker.html#modules)).

Decker has no `enum` type in Lil. The "enum-like" thing you are thinking of is the **`enum` contraption** below.

Enum-like contraptions
----------------------
Found in `dfxr`, `fonts`, `puppeteer` and `qr` (prototype `enum`); `imageEnum` is in `brushes`, `hershey`, `wigglykit` and `wigglypaint`.

| Prototype   | What it does                                                         |
| :---------- | :------------------------------------------------------------------ |
| `enum`      | "select from among enumerated string values." A compact slider plus a hidden field of options. |
| `imageEnum` | "select from among enumerated image values."                         |

`enum` attributes (from `puppeteer.deck`):

- `options` (type `code`): newline-separated list of choices. `get_options` / `set_options`.
- `value`: the currently selected string. `get_value` / `set_value`.
- Fires a `change` event with the selected string, so an instance script is `on change val do ... end`.
- Follows the card's `font`, `show` and `locked`.

Resizable (default 100x25). Underneath it is a slider whose `interval` is `0,(count options)-1` and whose `format` shows the selected label, so this is a good pattern to copy for any "pick one of N names" control.

Other contraptions
------------------
| Prototype        | Deck(s)               | Description |
| :--------------- | :-------------------- | :---------- |
| `animButton`     | wigglypaint           | A graphical drop-in replacement for buttons. |
| `toggleButton`   | wigglypaint           | A graphical drop-in replacement for checkboxes. |
| `rbutton`        | dialog                | A resizable rounded button. |
| `tabbar`         | cohostify             | A tab bar for an exclusive selection among several choices. |
| `spinner`        | enchilada             | Unbounded numeric picker. |
| `datePicker`     | enchilada, tour       | A monthly calendar date picker. |
| `patternPicker`  | enchilada, patedit    | A palette of mutable patterns, optionally with colors. |
| `clock`          | enchilada, tour       | A realtime clock (one version has a configurable UTC offset). |
| `dieRoller`      | enchilada, tour       | Rolls dice using `"1d6+5"` notation. |
| `viewCounter`    | enchilada             | Counts times the `view` event fires. |
| `dispatcher`     | enchilada             | Stops events bubbling from inside contraptions to the containing card. |
| `draggability`   | enchilada             | Contraption with an inner draggable thing. |
| `fancyBorder`, `bracket`, `paper`, `paintbox` | enchilada, tour, dialog | Decorative or resizable frames and backgrounds. |
| `enchilada`      | enchilada             | Demo of every attribute type. A good reference for `attributes`. |
| `scrollcanvas`   | hershey               | A scrollable, resizable viewport into an arbitrary-size inner canvas. |
| `scriptViewer`   | path, plot            | A tabbed editor for viewing and editing the scripts of widgets on the current card. |
| `palImport`      | color, palimport      | Imports `.hex` palettes as used by lospec.com. |
| `mover`          | sokoban               | A self-tweening sprite. |
| `follower`       | path                  | A semi-autonomous agent that animates itself along waypoints. |
| `popOut`         | wigglypaint           | A sliding element that alternates between two positions when clicked. |
| `ball`, `brick`, `paddle`, `wall` | breakout | Breakout game pieces; `ball` moves by velocity and bounces off overlapping contraptions. |
| `wiggler`        | wigglypaint           | A wiggly, squiggly animated drawing surface. |
| `wigglyStash`    | wigglypaint           | Saves a canvas temporarily and restores it later. |
| `wigglyCanvas`, `wigglyModal`, `wigglyPalette`, `wigglyPlayer` | wigglykit | The WigglyKit family: a drawing surface, a full image editor overlaid like a modal, 5-color palettes, and a player (also usable as a "Fancy Puppet" in Puppeteer). |
| `plyPlayer`      | twee                  | A self-contained player for Twine stories in the Ply format. |
| `buggo`, `smol`  | puppeteer, enchilada  | Small sprite/toy contraptions. |

Modules
-------
Modules are dictionaries of functions, available as a global named after the module. Lists below show functions I found in each script, not necessarily everything.

### Data, math and utilities

| Module  | Deck       | Description and notable functions |
| :------ | :--------- | :--------------------------------- |
| `stats` | stats      | Statistical measures for lists of numbers: `mode`, `midrange`, `quartiles`, `variance`, `std_dev`, `skewness`, `kurtosis`, plus population versions (`pvariance`, `pstd_dev`, ...). |
| `bn`    | bignums    | Arbitrary-precision arithmetic for natural numbers: `make`, `add`, `sub`, `mul`, `divmod`, `div`, `mod`, `equal`, `more`, `less`, `sumall`, `prodall`, `minall`, `maxall`, and formatters `format_plain`, `format_commas`, `format_name`. Works around Lil's fixed-precision numbers. |
| `rect`  | draggable  | Rectangle helpers on `pos`/`size` dictionaries: `make`, `overlaps`, `inside`, `constrain`, `union`, `intersect`. |
| `col`   | color      | Color manipulation: conversions (`from_comp`, `from_hsv`, `from_hex`, `from_css`, `to_css`), `closest` palette match, and a `cssnames` table. |
| `path`  | path       | Generic grid-based pathfinding, with `getpath` and cell/screen coordinate conversion. |
| `ease`  | ease       | Easing functions (e.g. `inBounce`, `outBounce`, `inOutBounce`) plus `tween`, `spline` and `spline_at` (Catmull-Rom). |

### Graphics and media

| Module | Deck | Description |
| :----- | :--- | :---------- |
| `plot` | plot | Draws graphs to canvases: `plot_line`, `plot_bar`, `plot_scatter`, `plot_hist`, `plot_box`, `plot_pie`, `plot_category`, `plot_series`, and data helpers `pivot`, `unpivot`. |
| `hershey` + `hf_*` | hershey | Read, write, render and manipulate Hershey vector fonts. The twelve `hf_` modules (futura, cursive, script, times, gothic, fraktur, with bold/italic variants) are the font data. |
| `qr` | qr | QR code generation, adapted from Kang Seonghoon's qr.js. Entry point `generate_code`. |
| `pdf` | pdf | Assembles PDF documents from Images and vector drawing streams. |
| `dfxr` | dfxr | Procedural sound-effect generator inspired by sfxr. |
| `ovals`, `sumis`, `stipplers`, `dirBrushes`, `stepBrushes`, `faeStamps`, `screenPrints`, `pens`, `wigglyBrushes` | brushes, wigglypaint, wigglykit | Collections of functional brushes for canvases. |

### Animation and presentation

| Module | Deck | Description |
| :----- | :--- | :---------- |
| `zazz` | zazz | Easy animation effects: `bob`, `wave`, `march`, `scroll`, `flipbook`, `inbox`, `path`, `lerp`. |
| `PublicTransit` | transitions, wigglypaint | Fancy transitions (`heart`, `star`, `circle`, `oval`, `clock`, `BarnHoriz`, `BarnVert`, ...). |
| `fancyTransitions` | enchilada | Heart and star wipes. |
| `utena` | utena | Iconic anime transitions. |
| `dd` | dialog, puppeteer | Sequential, styled modal dialogs for visual novels. |
| `pt` | puppeteer | Display and animate sprites for visual novels. |

### Text and formats

| Module | Deck | Description |
| :----- | :--- | :---------- |
| `twee` | twee | Manipulate and create Twine story files in the Twee 3 format. |
| `lil_syntax`, `octo_syntax` | cohostify | Convert Lil or Octo source into syntax-highlighted HTML. |
| `octo_emu` | chip8 | A basic CHIP-8 emulator. |

### "Dangerous" JavaScript bindings (`forbidden.deck`)
These only work in the web version of Decker and are deliberately kept in a separate deck. The deck warns that using them prevents the deck from working elsewhere.

| Module | Description |
| :----- | :---------- |
| `ajax` | Asynchronous HTTP requests. |
| `ls`   | Browser local storage. |
| `kb`   | Raw keyboard events. |
| `bgm`  | Looped background music from external media files. |

Patterns worth copying
----------------------
- **Contraption attributes**: define `get_x` / `set_x` in the prototype script, then list `x` in the prototype's `attributes` table (types include `code`, `data` and others; see [decker.md](decker.html#prototypeinterface)). `enum` and `enchilada` are the best examples.
- **Events out of a contraption**: `card.event["change" value]` is how `enum` notifies the host.
- **Modules own their state** through `data` (a keystore); they cannot touch the deck unless you pass widgets in as arguments.
- **Testing modules headlessly**: `import[]` a deck in Lilt to get its modules as a dictionary (see Modules in `decker.md`).

Caveats
-------
- This list covers only the decks in `examples/decks` at this commit. Decks on itch.io or elsewhere add more.
- Function lists were extracted by pattern matching on the scripts, so they may miss helpers defined in other ways. Read the module script before depending on a function.
