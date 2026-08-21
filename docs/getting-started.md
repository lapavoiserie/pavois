# Getting started

## An app

```bash
haxelib run mui init myapp    # scaffolds src/, mui.json, per-backend builds
cd myapp
haxelib run mui build cui     # or sui, wui, aui, pui — qui via haxe-sailfishos
haxelib run mui run cui
```

The scaffold is a complete app: `@:state`, `body()`, and `main()`. Add
surfaces as methods — see [the story](README.md) for the shapes, and
[mui's docs](https://lapavoiserie.github.io/mui/) for every view, prop and
binding.

## A companion surface

The networked corner is **off by default** — a Companion is served to other
machines, and no application gets that without asking. Ask in the build file:

```hxml
-D mui_cafos
```

Then, with a cafos agent running on the machine
([cafos GUIDE](https://github.com/lapavoiserie/cafos)):

```haxe
@:surface(Companion)
function panel():View { … }

// in main(), after construction — the second deliberate act:
var projector = cafos.mui.CompanionServe.serve(app);
app.lifetime.own(() -> projector.stop());
```

Without the define the declaration does not compile, and the refusal says
what to add: the framework never opens the network on your behalf.

Any machine serving a surface with that id renders the panel and sends taps
back. The sink side is a few lines around `cafos.nui.NuiSink` +
`nui.Snapshot.inflate` + any backend's `NodeRenderer` — see
`cafos/demo/nui-companion/SinkTui.hx` for a complete terminal sink.

## Going deeper, per library

| I want to… | read |
|---|---|
| know every view and prop | [mui](https://lapavoiserie.github.io/mui/) |
| understand signals, effects, lifetimes | [rui](https://lapavoiserie.github.io/rui/) |
| adopt the node model in a renderer | [nui](https://lapavoiserie.github.io/nui/) |
| add a native capability | [kui](https://lapavoiserie.github.io/kui/) |
| understand the network substrate | cafos (GUIDE.md, DESIGN.md) |
| target one platform deeply | that backend's own docs |
