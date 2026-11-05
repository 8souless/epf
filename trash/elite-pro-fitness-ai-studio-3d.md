# Elite Pro Fitness: AI Studio 3D scroll + web app prompt
Target tool: Google AI Studio, Build mode (assets already uploaded there by Bruno).
Assets: logo, team photo, fight-night corner, 1:1 promo flyer (owner in front of ring), coach story screenshot, Facebook profile flyer, 7 vertical phone clips (exterior x2, interior pan, front desk/bags, fight-night slideshow, probable duplicates).

## Change log
- 4 Nov 2026 v1: merged the Higgsfield scroll story (logo, exterior, walk in, ring, gym clips, owner, fight corner) with the 10-feature app spec into one AI Studio Build prompt. Scroll is built in Three.js inside the app, images restyled with Gemini's image model, location via Maps. Class timetable dropped (not in the current 10-feature list). Owner name left as a placeholder.

## Latest prompt
```
You are building a complete, working web app in AI Studio Build mode for a real community boxing gym. Build it in one go, don't ask questions, make sensible assumptions and list them in a README. Use only the facts and uploaded assets below; never invent names, prices, reviews, stats, opening hours or claims. Where a fact is missing, show an obvious editable placeholder in [square brackets].

## The client (real facts only)
- Name: Elite Pro Fitness - Boxing and Fitness Studio (logo text "Elite Pro Fitness, South Birmingham", short name "EPF").
- Address: 201A Merritts Brook Lane, Northfield, Birmingham B31 1UH.
- Phone: 07968 043030. Email: elitepro121@gmail.com.
- Owner / head coach: [Owner name] (placeholder, editable in settings).
- Classes: kids, women, adults, plus amateur competitors (competition squad).
- Socials: Facebook https://www.facebook.com/Epfgym, TikTok @ianwalker56. Instagram, YouTube, WhatsApp: empty editable fields.
- Opening hours and prices: unknown. Leave as owner-editable placeholders.

## Style
Dark, bold, gritty boxing look taken from the uploaded logo and 1:1 promo flyer: black background, red and white, gold only as a tiny accent. Bold condensed type, a subtle grit/film-grain texture, red rim light, haze. Taglines from the flyer: "Boxing | Fitness | Discipline | Real Results" and "Discipline builds freedom". Mobile-first, fully responsive, smooth animation everywhere.

## Step 1: regenerate the images
Use the Gemini image model available in this app (e.g. gemini-2.5-flash-image) to create cleaned-up, cinematic versions of each uploaded image, using the original as the reference image every time. Rules: keep the real people's faces, builds and clothing exactly; keep the real logo exactly (black text, red boxer silhouette raising both gloves); add no new text, people, logos or watermarks; style = moody dark gym lighting, red rim light, light haze, shallow depth of field, photorealistic.
- Logo: a clean, sharp, high-res version on transparent/black, plus a 3D-ready version (also recreate it as an SVG for the header, favicon and invoices).
- Promo flyer: the owner standing in front of the ring, hands behind his back, as a clean 16:9 hero still with the flyer text removed.
- Fight-night corner: the EPF boxer in the corner with the coach behind him, 16:9, arena spotlights and crowd haze.
- Team photo: the junior (white vests) and senior (black vests) squad inside the gym, cleaned and graded.
- From frames of the exterior clips: the gym front at night with the real sign ("ELITE PRO FITNESS, South Birmingham Amateur & Professional Boxing Club"), wet street reflections, 16:9.
- From frames of the interior clips: the front desk, the hanging heavy bags and the ring, 16:9 each.
- Don't show the coach story screenshot or the Facebook profile flyer anywhere; use them only as style and fact references.
Save the results as app assets and cache them so they're generated once, not on every page load. Put the generation in an owner-only "Regenerate visuals" button in Settings so it can be re-run. If generation fails or hasn't run, fall back to the original uploaded file so nothing breaks.

## Step 2: the public landing page = one continuous 3D scroll journey
Build the landing page as a single full-screen Three.js scene (use @react-three/fiber and @react-three/drei; ScrollControls or a GSAP ScrollTrigger-style scrub) where scrolling moves one camera along one smooth spline path, with no cuts, from outside the gym to inside. Scroll down = move forward, scroll up = move back. Each stop has short text that fades in and out with the scroll. Order:
1. Logo intro: the 3D logo floats in black space, slowly rotating, the red boxer glowing. Text: "Elite Pro Fitness, South Birmingham". A small "Scroll" hint.
2. Exterior: the camera pulls back and glides down a night street toward the gym front (regenerated exterior image on a lit 3D facade, wet ground reflections, light rain particles). The sign glows red as we approach. Text: the address.
3. Walking in: the camera pushes through the front doors, past the front desk and between hanging heavy bags that sway gently (simple 3D bags and chains textured dark red/black, plus the regenerated interior images as backdrop panels). Haze and dust particles in the light.
4. The ring: the ring is revealed ahead under overhead lights; the camera rises and orbits around it, ropes passing in the foreground. Text: "Kids | Women | Adults | Competition squad".
5. Gym clips: the uploaded phone clips play as floating, muted, looping vertical video panels around the ring, with poster images, lazy-loaded. Only these clips; don't stretch them full screen.
6. The owner: the camera settles in front of the regenerated owner hero still (in front of the ring), slow push-in with depth parallax, red light sweeping behind. Text: "1-to-1 sessions available" and a "Book a 1:1" button.
7. Fight corner: the camera slides past into darkness and comes out at fight night: the regenerated fight-corner image in a spotlit arena, slow orbit. Text: "Discipline builds freedom".
8. Finale: tilt up into the ring lights, flare to white, then resolve to the logo again with: a "Join" button (opens enrollment), the team photo (only if allowPublicPhotos is on), the social links as stacked animated icon buttons, the phone and email, and an embedded Google Map of 201A Merritts Brook Lane, Birmingham B31 1UH with a "Get directions" link.
Performance and accessibility: keep it smooth on phones (compressed textures, low poly, instanced particles, lazy video, cap pixel ratio, pause rendering when off-screen). With prefers-reduced-motion or on low-power devices, replace the 3D with a simple stacked page of the same sections and images. Keyboard navigable, alt text on every image, a "Skip intro" link straight to the finale.

## Step 3: the web app (exactly these 10 features, nothing else)
Two roles with simple login and seeded demo accounts: Owner (admin) and Member. Seed realistic demo data clearly marked as demo (about 40 members across kids, women, adults and competition squad, 4 weeks of attendance, invoices and payments), with no real names other than the gym's own.
1. Owner dashboard: animated KPI cards (active members, check-ins today, revenue this month, overdue payments, upcoming 1:1 sessions); charts for attendance over time, revenue by month, members by class type, active vs less-active members; quick actions (add member, open scanner, record payment). Header: a small slowly rotating 3D ring that never hurts performance.
2. Enrollments: register new members (name, date of birth, contact, emergency contact, class type, membership plan, start date, medical notes, waiver checkbox). Under-18s require parent/guardian details and a consent checkbox. Quick-add/import existing members; search, filter, edit, archive.
3. QR check-in attendance: each member gets a unique signed QR code on their profile (downloadable). A front-desk scanner page uses the camera (html5-qrcode) to check members in, with an animated green (OK) or red (expired subscription / already checked in today) result. Attendance drives an activity tier (Active / Less active / Inactive by check-ins in the last 30 days, thresholds configurable), a streak and a leaderboard.
4. Subscriptions: owner-defined plans (monthly, 10-class pass, pay-as-you-go, kids, women, adults) with owner-set prices; status active / expiring soon / expired, updated by payments.
5. Member fitness profiles: photo, class type, plan, subscription status, competition record (bouts, wins, losses, draws), weight class, a weight log with trend chart and fight-weight target, and fitness metrics (resting heart rate, 3 km run time, push-ups, skipping test, custom metrics) charted over time. Members log their own entries; the owner can view and edit.
6. One-to-one sessions: coaches set availability slots; members or the owner book; calendar view; statuses booked / done / cancelled / no-show; notes; an optional price that creates an invoice.
7. Custom training plans from an exercise database: seed at least 60 boxing exercises (footwork, bag work, pads, shadow boxing, conditioning, strength, core, mobility, sparring drills), each with description, sets, reps or time, difficulty and equipment. Drag-and-drop plan builder (days/weeks, sets, reps, rounds, rest). Assign to a member, who gets an in-app notification, ticks off sessions, and the owner sees progress.
8. Invoices: auto-generated on renewal and for paid 1:1 sessions; statuses draft / sent / paid / overdue; list with search and filters; PDF download with the logo (jspdf); payment history per member; monthly revenue report with CSV export.
9. Social links: owner manages the list (Facebook, TikTok, Instagram, YouTube, WhatsApp) shown as stacked animated icon buttons on the member home screen and the landing finale. Pre-filled: Facebook https://www.facebook.com/Epfgym, TikTok @ianwalker56.
10. Payments via the owner's existing QR method (no new payment processor): in Settings the owner uploads their existing payment QR image or pastes its payment link, plus the account name. At checkout the app shows that QR with the amount and a reference (member ID + invoice number). The member taps "I've paid"; the owner confirms in one tap; the invoice and subscription update instantly. Put this behind a PaymentProvider interface so a real provider could be added later, but build only the QR + owner-confirmation adapter.

## Privacy and security
- Photos may show minors: an allowPublicPhotos setting, default OFF, hides the team photo and any photo of people from public pages until the owner confirms consent. Never use kids' photos publicly without it.
- Hashed passwords, role-based routes, signed QR tokens, input validation (zod).

## Build notes
- React + TypeScript, Tailwind, Three.js via @react-three/fiber and drei, Framer Motion for UI, Recharts, qrcode + html5-qrcode, jspdf.
- If a separate backend can't run in this environment, keep a clean typed data layer and API-shaped service interface backed by browser storage, and say so in the README.
- Complete, runnable code, no "rest of code here". README: demo logins, assumptions, what the owner still needs to fill in (owner name, hours, prices, payment QR, other social handles, photo consent).
Build it now.
```
