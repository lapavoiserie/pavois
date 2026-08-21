# Pavois

**Write an application once, in one vocabulary. It runs native on six
platforms — and its surfaces live wherever your network has room for them.**

Pavois is the umbrella over La Pavoiserie's application framework: a family
of small Haxe libraries that together cover what an application *is* —

- a **shared vocabulary** of views, state and declarations (`mui`, `rui`,
  `nui`),
- **six native backends** that render it — SwiftUI on Apple (`sui`), Compose
  on Android (`aui`), WinUI 3 on Windows (`wui`), Qt/Silica on Sailfish OS
  (`qui`), a terminal UI (`cui`), and an owner-drawn engine (`pui`),
- a **capability substrate** for what apps need from the platform (`kui`),
- and a **network substrate** for presence, transport, auth and fluidity
  across machines ([cafos](https://github.com/lapavoiserie/cafos)).

The name is the naval gesture: *pavoiser* is to dress a ship with flags. An
application's **surfaces** — its window, its cover, its menus, its remote
panels — are its flags; the machines around you are the masts. Declaring a
surface hoists it wherever there is a place for it. An app with every surface
flying, across every machine, is *en grand pavois*.

## Documentation

The story in one place: **[docs/](docs/)** (docsify — serve locally or via
Pages). Each library keeps its own detailed docs; the umbrella tells you how
they fit.

## Status

The surface model is implemented and validated on-device across Sailfish,
macOS, Windows and the terminal; the Companion role projects live surfaces
across processes and machines over cafos. Widget snapshots (iOS/Android) are
the next chantier.
