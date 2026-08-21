# The story

An application is not one render root. It has a main window — and, depending
on where it runs, a cover on the task switcher, a menu bar, a settings pane,
extra windows, a panel on the machine across the room. Pavois calls each of
those an **app surface**, and it is built on one idea:

> **Declare a surface once, in the shared vocabulary. Every platform mounts
> it on what it actually has — and where a platform has nothing to mount it
> on, the build says so, at the declaration, naming the platform.**

```haxe
class TodoApp extends mui.App {
	@:state var todos:ImmutableList<Todo> = ImmutableList.empty();

	override function body():View { … }        // the main window, everywhere

	@:surface(Glance)                          // the Sailfish cover, live
	function glance():View { … }

	@:surface(Commands)                        // ⌘-menu on macOS, key
	function shortcuts():Array<Command> { … }  // bindings on a terminal,
	                                           // a MenuBar on Windows
	@:surface(Preferences)                     // the macOS Settings scene
	function preferences():View { … }

	@:surface(Companion)                       // a live panel on another
	function panel():View { … }                // machine, over the network
}
```

The same file, compiled six ways, is a Mac app with a real menu bar and a
Settings pane, a Windows app with extra windows, a Sailfish app whose cover
stays live in the task switcher, a terminal app with key bindings — and, on
any of them, its `Companion` panel can appear on another machine entirely,
rendered there, its buttons running *your* closures back home.

Reading `@:state` inside a surface keeps it live. That is the whole
reactivity contract, and it holds identically for a window, a cover and a
panel on the other side of the network.

Portable does not mean silent. Each backend states the roles it hosts, and a
declaration with no host on the target you are building **stops that build**,
naming the role and the backend — because what a compiler can know, a
compiler should say. Accepting a gap is then a line in your own source:

```haxe
@:surface(Glance, optional)     // the Sailfish cover — and this app accepts
function today():View { … }     // that it flies nowhere on the others
```

## En grand pavois

*Pavoiser* is to dress a ship with flags. Your surfaces are the flags; the
machines around you are the masts. (The miniature hoist beside the wordmark
is the real thing: the six International Code of Signals flags that spell
P·A·V·O·I·S — Papa leading, the Blue Peter, "about to sail".) An application with every declared surface
flying — window here, cover there, panel across the room — is *en grand
pavois*. The framework's job is to make hoisting them one line each, and to
strike them cleanly when a mast disappears.

## What exists today

| Surface | Where it is live |
|---|---|
| Main window | every backend |
| Cover (Glance) | Sailfish — live-mounted, survives recreation |
| Menu / commands | macOS menu bar (⌘-shortcuts), Windows MenuBar, terminal bindings |
| Settings (Preferences) | macOS Settings scene (⌘,) |
| Extra windows (Auxiliary) | Windows, macOS — one per declaration |
| Remote panel (Companion) | any machine on the cafos network, served from any backend |
| Widgets (Glance on iOS/Android) | next — the snapshot chantier |

Start with [Architecture](architecture.md) for how the pieces fit, or
[Getting started](getting-started.md) to build something.
