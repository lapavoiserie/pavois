# Architecture

Pavois is a family of deliberately small libraries. Each does one thing, each
has its own repository and documentation; this page is the map. For the
same map with a step-through of a tap crossing every layer, read
[Layer by layer](onboarding/index.html ":ignore").

```
                     your application
                          │
              ┌───────────┴───────────┐
              │          mui          │   the portable vocabulary:
              │  views · @:state ·    │   29 names, roles, @:surface,
              │  @:surface · Contract │   resolved onto ONE backend
              └───────────┬───────────┘
        ┌───────┬─────┬───┴───┬─────┬───────┐
      sui     aui    wui    qui    cui    pui      six native backends
    SwiftUI Compose WinUI  Silica  TUI  self-drawn
        └───────┴─────┴───┬───┴─────┴───────┘        ┌─────────┐
              ┌───────────┴───────────┐              │   dui   │  the halyard:
              │      rui  ·  nui      │◄─────────────│ carries │  where a surface
              │  signals/effects/     │              │ surfaces│  goes, and to whom
              │  lifetime · node model│              └────┬────┘
              └───────────┬───────────┘                   │
         ┌────────────────┴────────────────┐              │
         │   kui              cafos        │◄─────────────┘
         │   native            network     │   the substrates:
         │   capabilities      presence,   │   platform capabilities;
         │   (store, wear)     links, auth │   presence, transport, identity
         └─────────────────────────────────┘
```

## The layers

**[mui](https://lapavoiserie.github.io/mui/)** — the portable layer an
application writes against. There is no `mui.App` class: `mui` is a
*contract plus a resolver* — every name (`mui.View`, `mui.ui.Button`,
`mui.App`) is an alias resolved at compile time onto the one backend the
build selects (`-D mui_backend=…` + `--macro mui.macros.Bind.all()`), and
the contract is checked. Surfaces, roles, the `@:surface` sugar and the
`@:hostedRoles` refusal live here, as does the `Describe` register every
backend signs. Nothing in `mui` names a backend; adding a seventh touches
zero files there.

**The six backends** — each is an independent library that renders the
vocabulary with its platform's real widgets, and *hosts* the surface roles
its platform has, stated as `@:hostedRoles` on its `mui.App`:

| lib | platform | renders with | hosts |
|---|---|---|---|
| [sui](https://lapavoiserie.github.io/sui/) | macOS · iOS · visionOS | SwiftUI, built at runtime from the Haxe tree | Preferences, Auxiliary, Commands, Glance (WidgetKit), Companion |
| [aui](https://lapavoiserie.github.io/aui/) | Android · Wear OS | Jetpack Compose; Haxe on the JVM | Glance (App Widget), Companion — and the far side of one |
| [wui](https://lapavoiserie.github.io/wui/) | Windows | WinUI 3, through the push contract | Auxiliary, Commands (MenuBar), Companion |
| qui | Sailfish OS | Qt/Silica, in `haxe-sailfish` (private) | Glance — the cover, mounted *live* |
| [cui](https://lapavoiserie.github.io/cui/) | a terminal | a cell grid | Commands (key bindings), Companion |
| pui (private) | browser, desktop, mobile, Sailfish | its own drawing — one look everywhere | Companion |

**[rui](https://lapavoiserie.github.io/rui/)** — the reactive core: signals,
effects, `Lifetime`, `State` with its platform and durable sinks, the
scheduler (synchronous by contract, with a `batch` so one gesture is one
render), and the view rule — "a view reads only immutable or observable
state" — enforced at compile time. Every surface, local or remote, is one
effect over the shared signal graph.

**[nui](https://lapavoiserie.github.io/nui/)** — the shared node model, with
three contracts: **pull** (a host walks the app's tree), **push** (the app
drives a sink), and **snapshot** (the tree as pure data, closures replaced
by action ids keyed by *place* — what crosses a process or machine
boundary). `nui.Follow` keeps a snapshot surface current without the
application asking; `nui.SelfSource` lets a backend draw a tree that
arrived.

**dui** (private) — the halyard. `nui.Follow` decides *when* a fresh
picture exists; `dui` decides *where it goes*: a transport contract that
names its target, targets as observable state so a picker can show them,
pairings remembered per surface, and a default reach — `Paired` — under
which nothing leaves the device until somebody names a destination. Two
transports today: `dui.cafos` to a machine on the network, `dui.wear` to a
paired watch. State never crosses; pictures do.

## The substrates

**[kui](https://lapavoiserie.github.io/kui/)** — native capabilities, one
implementation per platform, reused by every backend, wired into each
platform's build through five link channels (hxcpp, qmake, xcode, gradle,
msbuild). Two ship as their own repositories: **kui-store**, the durable
key-value store behind `@:state(durable)`; **kui-wear**, messages to and
from a paired watch, with the manifest-declared service that receives while
the app is not on screen.

**cafos** (private) — the network substrate: which machines and surfaces
exist *here and now* (a replicated, single-writer registry), how to reach
them (an opaque, encrypted, agent-relayed channel), who may (Ed25519
identities, enrolment, per-surface policy), and fluidity — content that
follows surfaces as they come and go. It knows nothing about a `nui.Node`,
by design. To Pavois it is what `kui` is for platform capabilities: the
substrate underneath.

## The off-device corner is opt-in, three times

A `Companion` surface leaves this device, and nothing about writing an
application implies wanting that. Three deliberate acts, none a default:
`-D mui_carry` in the build file (the older spelling `mui_cafos` still
works), the explicit `dui.mui.CompanionServe.serve` call, and a pairing.

## The rules the family keeps

A few conventions repeat in every library, and they are load-bearing:

- **What can be known at compile time is never a marker on screen** — but a
  tree received *as data* degrades with a word, never a crash.
- **Identity is the place, never the pointer** — node identity, focus,
  action ids across generations.
- **Degradation is declared, not accidental** — `@:surface(Role, optional)`,
  a contract entry a backend leaves out, a capability answering `null`.
- **One record per surface** — its own effect, its own lifetime, its own
  action table; never a shared static registry.
- **One gesture, one render** — every backend opens a batch where a host
  event arrives; state sinks are never delayed by it.
- **A widget is proven by its picture** — a view-tree oracle proves the
  pipeline ran, not that anyone can see the result.
