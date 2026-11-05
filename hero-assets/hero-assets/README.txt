ELITE PRO FITNESS - landing hero assets (continuous-scroll hero)
Theme: black / red / white. Page background gradient #2a0508 -> #050505.
Every image has a .webp copy (quality 82) for the web; PNG/JPG are the masters.

STEP 1 - Logo on the disc
  logo-3d.png (2048x2048, transparent)   3D stacked logo: red boxer on top, white text below. Built in PIL from the real logo pixels (no redrawing, no AI).
  logo-3d-turntable/frame_00..23.png     24-frame +/-45 degree sway of logo-3d (1024x1024, transparent); loop 00->23 for a gentle 3D turn.
  logo-stacked.png (2048x2048)           Flat fallback of the same stacked layout (white text).
  logo.png (2048x2048)                   Original horizontal logo, black text (for light backgrounds).
  england-boxing-logo.png (1024x1024)    England Boxing badge, transparent (affiliation strip/footer).

STEP 2 - Hover cards
  cards.png (2336x1744 sprite)           Four 1150x810 tiles at x,y: [0,0] coach-bg, [1186,0] corner, [0,900] outside, [1186,900] coach-bg close crop.
  coach.png (1534x3246, transparent)     The coach cut out of the promo poster (real pixels).
  coach-bg.jpg (1920x1080)               The coach in front of the ring (poster crop, no text).
  corner.jpg (1920x1440)                 Fight-night corner, wide; fighter's face blurred, coach unchanged.

STEP 3 - Land / Fore parallax
  outside.jpg (2560x1440)                LAND layer: the real gym exterior (Bruno's daytime photo, cleaned + graded, cropped to 16:9).
  fore.png (2560x1440, transparent)      FORE layer: the pavement only, pixel-aligned with outside.jpg.
  Stack: outside.jpg -> the word 'NORTHFIELD' -> fore.png (same size and position) so the text sits behind the pavement edge.

preview.jpg                              Contact sheet of all assets.
