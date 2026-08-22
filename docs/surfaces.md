# Surfaces

The surface model is Pavois's central idea. The full reference lives in
[mui's Surfaces page](https://lapavoiserie.github.io/mui/#/surfaces); this
page is the conceptual map.

## The three axes

A surface is a corner of a cube:

- **Content** — a living *tree* of views, or a typed *model* (a command set,
  a notification) mapped to a native API.
- **Update** — *live* (an effect reconciles on state change) or *snapshot*
  (the system samples a render function when it decides to).
- **Residence** — *co-resident* (our process, reading signals directly) or
  *detached* (another process or machine, fed serialized state).

The main window, the Sailfish cover, a macOS Settings pane and an extra
window all share the **live co-resident** corner: one effect per surface over
one shared signal graph. A Companion panel is **live detached**: the same
effect, projecting snapshots over the network. An Android widget is
**snapshot detached**, and that corner is now built: the surface is *sampled*
into the same pure data a Companion frame carries, the launcher stores the
picture — so it outlives the process that drew it — and a tap on it comes back
as an action id that resolves to the closure it named. iOS (WidgetKit) is
next, on the same contract.

### Who decides when a snapshot is taken

That is the one question the live corner never has to ask. A live surface
reconciles itself; a sampled one is drawn when the *system* decides, which on
a home screen means once, at binding, and then never again on its own. So the
application gets a way to say *now* — one sentence, said the same to every
host:

```haxe
mui.surface.Resample.request(Glance);
```

Android pushes a fresh picture into the widget's state, WidgetKit calls
`reloadTimelines`, a self-drawn painter repaints. And on a backend that hosts
no such surface the call **is not compiled at all** — which is not a silence,
because the declaration itself could not have compiled there without saying
`optional`, the line where the application accepted that this surface flies
nowhere on that target. One application, four builds, one sentence that means
exactly what it can mean on each.

## Roles, not native surfaces

Applications declare *roles* (`Glance`, `Commands`, `Preferences`,
`Auxiliary`, `Companion`…), never native surfaces — a cover, a widget and a
live tile are the same role wearing different clothes. Each backend maps the
roles its platform has, and states them where the compiler can read them
(`@:hostedRoles`): declaring a role your target cannot host stops the build,
naming both, and accepting the gap is an explicit `@:surface(Role, optional)`
in your own source. Cardinality is the host's answer: one cover per app on
Sailfish, as many extra windows as you declare on Windows.

## The lifecycle every host implements

```
Declared → Waiting → Attached ⇄ Detached → Disposed
```

The framework owns the states; each host implements the transitions. The
Sailfish cover was the proving ground — a container that does not exist at
startup, is created lazily, and is destroyed and recreated behind the app's
back — and the network generalizes the same machine: a cafos surface's
`connected` flag *is* Waiting/Attached/Detached, with delta catch-up.

## The detached wire

The whole detached-over-network corner is opt-in: a build that has not set
`-D mui_cafos` cannot even declare a `Companion`. Pavois is a way to write
native applications *and* a way to let their surfaces live on other machines,
and the second never arrives by default with the first.

A live tree cannot leave the process — its props carry closures. Crossing a
boundary means the [snapshot contract](https://lapavoiserie.github.io/nui/#/snapshot):
the tree as pure JSON-safe data, every closure replaced by an action id that
is **stable by place** (same button, same id, across generations — a tap
racing a re-render does what the unchanged button says). On the far side the
snapshot inflates back into ordinary nodes, and any backend's `NodeRenderer`
draws it — the renderer cannot tell the tree came off a wire.

Each backend contributes its **describer** — its views as canonical nodes —
so a tree served from a Mac app and one served from a terminal app look the
same on the wire.

## Where this goes

The [cafos fluidity model](https://github.com/lapavoiserie/cafos) already
lets content *follow* surfaces — "on the phone if it is present, else on the
Mac", with state preserved. Bringing that placement language to Pavois
surfaces is the roadmap's horizon: the OS gesture — deciding what shows
where, as the world changes — applied to every machine you own.
