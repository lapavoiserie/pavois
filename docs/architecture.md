# Architecture

Pavois is a family of deliberately small libraries. Each does one thing, each
has its own repository and documentation; this page is the map.

```
                     your application
                          │
              ┌───────────┴───────────┐
              │          mui          │   the portable vocabulary:
              │  views · @:state ·    │   21 views, roles, @:surface,
              │  @:surface · Contract │   resolved onto ONE backend
              └───────────┬───────────┘
        ┌───────┬─────┬───┴───┬─────┬───────┐
      sui     aui    wui    qui    cui    pui      six native backends
    SwiftUI Compose WinUI  Silica  TUI  owner-drawn
        └───────┴─────┴───┬───┴─────┴───────┘
              ┌───────────┴───────────┐
              │      rui  ·  nui      │   the shared cores:
              │  signals/effects/     │   reactivity, and the node
              │  lifetime · node model│   model + its 3 contracts
              └───────────┬───────────┘
         ┌────────────────┴────────────────┐
         │   kui              cafos        │   the substrates:
         │   native            network     │   platform capabilities;
         │   capabilities      presence,   │   presence, transport,
         │                     transport,  │   auth, fluidity
         │                     auth        │
         └─────────────────────────────────┘
```

## The layers

**[mui](https://lapavoiserie.github.io/mui/)** — the portable layer an
application writes against. There is no `mui.App` class: `mui` is a
*contract plus a resolver* — every name (`mui.View`, `mui.ui.Button`,
`mui.App`) is an alias resolved at compile time onto the one backend the
build selects, and the contract is verified structurally. Surfaces, roles and
the `@:surface` sugar live here, as does the `Describe` register every
backend signs.

**The six backends** — each is an independent library that renders the
vocabulary with its platform's real widgets, and *hosts* the surface roles
its platform has:

| lib | platform | renders with | notable hosts |
|---|---|---|---|
| [sui](https://lapavoiserie.github.io/sui/) | macOS · iOS · visionOS | SwiftUI (dynamic runtime walk) | Settings scene, menu bar, extra windows |
| [aui](https://lapavoiserie.github.io/aui/) | Android | Jetpack Compose (Haxe on the JVM) | — (widgets next) |
| [wui](https://lapavoiserie.github.io/wui/) | Windows | WinUI 3 (push contract) | MenuBar, extra windows |
| qui | Sailfish OS | Qt/Silica (in haxe-sailfish) | the live cover |
| [cui](https://lapavoiserie.github.io/cui/) | terminal | cell-grid TUI | command key bindings |
| [pui](https://lapavoiserie.github.io/pui/) | anywhere it can paint | its own drawing (Canvas2D, CoreGraphics, Direct2D, QPainter…) | both ends of the Companion wire |

**[rui](https://lapavoiserie.github.io/rui/)** — the reactive core: signals,
effects, `Lifetime` (ownership and the `keep` view-lifetime), and the view
rule ("a view reads only immutable or observable state", enforced at compile
time). Every surface, local or remote, is one effect over the shared signal
graph.

**[nui](https://lapavoiserie.github.io/nui/)** — the shared node model, with
three contracts: **pull** (a host walks the app's tree), **push** (the app
drives a sink), and **snapshot** (the tree as pure data, closures replaced by
stable action ids — what crosses a process or machine boundary).

## The substrates

**[kui](https://lapavoiserie.github.io/kui/)** — native capabilities, one
implementation per platform, reused by every backend, wired into each
platform's build system through five link channels.

**[cafos](https://github.com/lapavoiserie/cafos)** — the network substrate:
which machines and surfaces exist *here and now* (a replicated registry),
how to reach them (an opaque, encrypted, agent-relayed channel), who may
(Ed25519 identities and enrollment), and fluidity — content that follows
surfaces as they come and go. Pavois rides it for the `Companion` role — a
corner that stays off until a build asks for it (`-D mui_cafos`): nui
snapshots over the opaque channel, rendered by any backend's `NodeRenderer`
on the far side. cafos keeps its own identity and roadmap; to Pavois it is
what kui is for platform capabilities — the substrate underneath.

## The rules the family keeps

A few conventions repeat in every library, and they are load-bearing:

- **What can be known at compile time is never a marker on screen** — but a
  tree received *as data* degrades with a word, never a crash.
- **Identity is the place, never the pointer** — node identity, focus,
  action ids across generations.
- **Degradation is declared, not accidental** — `@:muiSupport`, host
  `capabilities()`, the role no-op.
- **One record per surface** — its own effect, its own lifetime, its own
  action table; never a shared static registry.
