# dubai-3d-explore-map

Dubai 3D Interactive Map

A stylised, low-poly 3D map of Dubai in a single standalone HTML file. No build step, no dependencies to install, no server required — open the file in a browser and explore.

<img width="1397" height="659" alt="image" src="https://github.com/user-attachments/assets/56945cdd-5bfb-4401-a77b-cd41d3ae9a74" />
<img width="1397" height="659" alt="image" src="https://github.com/user-attachments/assets/d1ba28c7-455c-4421-a49f-cb34c66deb82" />
<img width="1397" height="659" alt="image" src="https://github.com/user-attachments/assets/10780805-dc53-4e76-b1c3-5b8660857905" />


Features
Five hero landmarks

Hand-modelled procedural geometry, each clickable with an info card:

Burj Khalifa — Y-plan tri-wing profile with six telescoping setbacks, hex core and spire
Burj Al Arab — extruded sail silhouette on its own island, with helipad and mast
Palm Jumeirah — 17 tapered fronds, crescent breakwater, Atlantis with skybridge, trunk apartments
Ain Dubai — observation wheel on Bluewaters Island: rim, 24 spokes and capsules, A-frame legs
Museum of the Future — calligraphy-textured torus on a landscaped hill
Districts
Downtown — Burj Lake with fountain jets, Dubai Mall, Souk Al Bahar, Dubai Opera, ten podium towers, lawns and tree-lined plazas
Bluewaters Island — rounded island slab, promenade, residential blocks, pier and boats
Three modes
Mode	Camera	Audio
Explore	Free orbit / pan / zoom (mouse or touch)	Silent
Helicopter Tour	High, faster, closed loop over all five landmarks, with smooth altitude swell and gentle banking into turns	Procedural rotor: sub-bass rumble, 12 Hz gated blade chop, thin wind hiss
Yacht Tour	Low over the water, slower, coastal route that ping-pongs end-to-end, with non-cumulative bob and sway and a low-poly bow in view	Procedural sea: lowpass wave wash with a slow breathing swell, soft wind

Tour controls: Pause/Resume, Prev/Next landmark, Mute, Exit. Switching tours cross-fades cleanly — the two soundscapes never overlap.

Road network

Referenced against the real RTA/OSM layout: E11 Sheikh Zayed Road (with elevated flyover and ramps), E44, E311, Jumeirah Beach Road, Financial Centre Road, Umm Suqeim Street, Al Sufouh connector, the Palm trunk road, the Burj Al Arab causeway, the Bluewaters bridge — every road terminates on another road — plus a drivable Mohammed bin Rashid Boulevard loop threading between the Downtown towers. Skyline blocks are procedurally placed but excluded from every carriageway and elevated deck.

Environment

Single sun anchored over the Gulf with one aligned water-glitter reflection, horizon haze band, and a seeded skyline (~550 instanced blocks) that renders identically on every load.

Getting started
bash
git clone https://github.com/<you>/<repo>.git
cd <repo>
# then just open the file:
open dubai-3d-fixed-v5.html        # macOS
start dubai-3d-fixed-v5.html       # Windows
xdg-open dubai-3d-fixed-v5.html    # Linux

Or double-click the file. The only network request is the Three.js r128 CDN script, so you need to be online on first load.

Deploy on GitHub Pages
Rename the HTML file to index.html
Settings → Pages → deploy from the main branch root
Your map is live at https://<you>.github.io/<repo>/
Controls
Input	Action
Left-drag / one finger	Orbit
Right-drag / two fingers	Pan
Scroll / pinch	Zoom
Click a landmark or menu item	Fly to it and open its info card
Tour buttons (bottom)	Start Helicopter or Yacht tour, or return to Explore

Audio starts only after you tap a tour button (required for mobile autoplay policies; includes an iOS Safari silent-buffer unlock).

Technical notes
Three.js r128 from CDN with OrbitControls; everything else is hand-rolled in one inline <script>.
Procedural everything — geometry, textures (canvas-generated calligraphy, sun glow, glitter streak, horizon gradient) and audio. There are no image, model or sound assets.
Web Audio graphs are lazily built once per tour and reused; LFOs modulate inner gain stages while start/stop/mute only ramp outer masters, so silence is genuinely silent and switching never duplicates nodes.
Seeded RNG (LCG, fixed seed) makes the generated skyline deterministic across loads.
Tour cameras ride arc-length-parameterised Catmull-Rom splines. The helicopter loop is closed with modulo-normalised time (robust to tab-backgrounding delta spikes); the yacht route is open and reverses direction at each end instead of teleporting.
The world group is mirrored on X to match real-world orientation; hero landmarks live in world space with baked positions.
Browser support

Any modern desktop or mobile browser with WebGL. Tested layouts are responsive; the yacht bow, tour HUD and cards adapt to small screens.
