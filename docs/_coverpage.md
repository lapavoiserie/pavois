<div class="hoist" aria-hidden="true">
<svg viewBox="0 0 640 150" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Six international signal flags spelling PAVOIS, hoisted on a dressing line">
  <!-- the dressing line -->
  <path d="M8 30 Q 320 6 632 30" fill="none" stroke="#5a6a7e" stroke-width="1.5"/>
  <!-- P · Blue Peter -->
  <g transform="translate(40 28) rotate(-1.6)">
    <line x1="32" y1="-9" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="64" height="48" fill="#1B4B8F"/>
    <rect x="18" y="13.5" width="28" height="21" fill="#f4f7fb"/>
  </g>
  <!-- A · Alfa (swallowtail) -->
  <g transform="translate(136 22) rotate(1.2)">
    <line x1="32" y1="-8" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <polygon points="0,0 32,0 32,48 0,48" fill="#f4f7fb"/>
    <polygon points="32,0 64,0 50,24 64,48 32,48" fill="#1B4B8F"/>
  </g>
  <!-- V · Victor (red saltire) -->
  <g transform="translate(232 26) rotate(-0.8)">
    <line x1="32" y1="-10" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <clipPath id="victor"><rect width="64" height="48"/></clipPath>
    <rect width="64" height="48" fill="#f4f7fb"/>
    <path d="M0 0 L64 48 M64 0 L0 48" stroke="#C8102E" stroke-width="11" clip-path="url(#victor)"/>
  </g>
  <!-- O · Oscar (red over yellow, diagonal) -->
  <g transform="translate(328 22) rotate(1.5)">
    <line x1="32" y1="-8" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <polygon points="0,0 64,0 0,48" fill="#C8102E"/>
    <polygon points="64,0 64,48 0,48" fill="#EBB410"/>
  </g>
  <!-- I · India (black roundel on yellow) -->
  <g transform="translate(424 27) rotate(-1.2)">
    <line x1="32" y1="-11" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="64" height="48" fill="#EBB410"/>
    <circle cx="32" cy="24" r="11" fill="#0d1523"/>
  </g>
  <!-- S · Sierra -->
  <g transform="translate(520 23) rotate(0.9)">
    <line x1="32" y1="-9" x2="32" y2="2" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="64" height="48" fill="#f4f7fb"/>
    <rect x="18" y="13.5" width="28" height="21" fill="#1B4B8F"/>
  </g>
</svg>
</div>

# Pavois

> Every surface, every mast.

<p class="cover-lede">Write an application once, in one vocabulary. It runs
native on six platforms — and its surfaces live wherever your network has
room for them.</p>

<div class="signal-grid">
  <div><b>One vocabulary</b><span>views · <code>@:state</code> · <code>@:surface</code> declarations</span></div>
  <div><b>Six native backends</b><span>SwiftUI · Compose · WinUI 3 · Qt/Silica · terminal · owner-drawn</span></div>
  <div><b>Beyond the window</b><span>covers, menus, settings, extra windows, remote panels</span></div>
  <div><b>A networked substrate</b><span>presence, transport, auth, fluidity — via <code>cafos</code></span></div>
</div>

[The story](README.md)
[Architecture](architecture.md)
