<div class="hoist" aria-hidden="true">
<svg viewBox="0 0 640 118" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The six international code flags spelling PAVOIS, hoisted on a dressing line">
  <!-- the dressing line -->
  <path d="M8 30 Q 320 8 632 30" fill="none" stroke="#5a6a7e" stroke-width="1.5"/>
  <!-- Geometry is the ICS chart's own: square flags; Papa/Sierra inner
       square one third; Alfa notch to three quarters; Victor saltire
       17.5% of the side; India roundel a quarter; Oscar per bend,
       red upper fly, yellow lower hoist. -->
  <!-- P · Papa -->
  <g transform="translate(46 26) rotate(-1.6)">
    <line x1="26" y1="-8" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="52" height="52" fill="#1B4B8F"/>
    <rect x="17.33" y="17.33" width="17.34" height="17.34" fill="#f4f7fb"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">P</text>
  </g>
  <!-- A · Alfa (swallowtail) -->
  <g transform="translate(142 21) rotate(1.2)">
    <line x1="26" y1="-7" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <polygon points="0,0 52,0 39,26 52,52 0,52" fill="#f4f7fb"/>
    <polygon points="26,0 52,0 39,26 52,52 26,52" fill="#1B4B8F"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">A</text>
  </g>
  <!-- V · Victor (red saltire) -->
  <g transform="translate(238 25) rotate(-0.8)">
    <line x1="26" y1="-9" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <clipPath id="victor"><rect width="52" height="52"/></clipPath>
    <rect width="52" height="52" fill="#f4f7fb"/>
    <path d="M0 0 L52 52 M52 0 L0 52" stroke="#C8102E" stroke-width="9.1" clip-path="url(#victor)"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">V</text>
  </g>
  <!-- O · Oscar (per bend: red upper fly, yellow lower hoist) -->
  <g transform="translate(334 21) rotate(1.5)">
    <line x1="26" y1="-7" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="52" height="52" fill="#C8102E"/>
    <polygon points="0,0 0,52 52,52" fill="#EBB410"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">O</text>
  </g>
  <!-- I · India (black roundel on yellow) -->
  <g transform="translate(430 26) rotate(-1.2)">
    <line x1="26" y1="-10" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="52" height="52" fill="#EBB410"/>
    <circle cx="26" cy="26" r="13" fill="#0d1523"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">I</text>
  </g>
  <!-- S · Sierra -->
  <g transform="translate(526 22) rotate(0.9)">
    <line x1="26" y1="-8" x2="26" y2="1" stroke="#5a6a7e" stroke-width="1"/>
    <rect width="52" height="52" fill="#f4f7fb"/>
    <rect x="17.33" y="17.33" width="17.34" height="17.34" fill="#1B4B8F"/>
    <text x="26" y="70" text-anchor="middle" class="hoist-letter">S</text>
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
