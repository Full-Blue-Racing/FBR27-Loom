# Milspec Harnessing / Wiring Harnesses

*Notes from HP Academy Rob Dahm videos — 10/8/26. Physical version transcribed by our friend Panu from BCU. Markdown file prepared by yy.*

## Intro & Planning

**3 levels of wiring harness:**

1. Multi-spray[?] stock OEM harness — **(Level 1)**
2. Custom harness but no shielding, varying wires, additional bad crimps etc. / BM heatshrink on connector, e.g. rubber wires exposed (perhaps not shielded) — **(Level 2.5)** *flying leads*
3. **Milspec** — expensive *capacity heatshrink / vacuum sheath · DR25 and Tefzel wire · adhesive to oil/water-proof harness*

**Harnesses for cars:**
**Oils, fuels, coolant can leak onto harness — goal is to protect wires.**

- **Strain relief** — protection from harness pulling on wires.
- **Milspec** — adhesive where wires join inside the DR25 crawling[?] sheath / snake skin, to prevent ingress. *(more strands)*
- **Milspec** — Tefzel wire; same wire cores inside, just thinner — country[?] cross[?] smaller wire for same gauge — handles heats, alcohols etc.

**Planning / writing phase**

- Go to ECU documentation and look at wiring diagrams.
- Draw out harness and rope lengths / direction of harnesses from ECU to components, to firewall bulkhead etc.
  - e.g. `ECU — 12" / 16" / 18" / 20" / 10" / 6" — Firewall — INJ (1 2 3 4) … CAN`
- For above, component / sensor / functional actuators list required.
  - e.g. **Sensors** | **Actuators** — INJ, IGNI, WG, CANBUS, GNDS, PWRS

> Annotation: *Slave to Failsafe[?] if a build to the dashboard, so future plans are valid.*

---

## Harness Design & Concentric Twisting

(wth i can barely read the first few lines)

**Milspec harnessing and wiring design.**

Begin arranging: thicker gauge for **power**, thinner for **sensors**, and separating harness entries (?) checks for anything plugged in in place.

**Every core section of the engine harness (any harness) starts the same way:**

**1. Where is the engine at?** — *not the block*

- Where in terms of rotation; if just launch:
  > INJ firing off / IGN? firing off / sensors can't calibrate yet
  >
- **Trigger wheel** — teeth like [sketch]
  - ⟵ **CRANK ANGLE SENSOR** *(red note)*
  - When moving past a magnetic sensor, the protrusions stick / create resistance which can be sensed.
  - Every trigger wheel has an extended gap [sketch].
  - Able to discern how far in rotation as a zero[?] point of engine rotation.
  - Information is very sensitive to rest of the car.

**i. Centre of harness** is the thing that needs to be most protected from EMF etc. → **shielded wire** used to protect data transmission in the cable.

- Any EMI in the harness could affect unshielded wire data. (Note that any loop in circuit has the capaiblity of generating EMF.)
  > *As Andrew says, ignition coils most likely to interfere — i.e. at high RPM and large IGNI coil footprint* → *bits and bytes → message gets scrambled — NaN values etc.*
  >
- Shielded wire means nothing unless it is grounded.
- What matters in a harness with shielded wire is the centre of the harness ⟵ inflexible, so better in centre and better to protect.

**2. Concentric Twisting (Unlikely to be used in FBR harness as difficult to modify)**

- "Fancy braiding" — i.e. wrapping wires around a shielded core. Helps organise, looks pretty, and prevents EMI — e.g. where ignition and trigger-wheel sensor wires are next to each other (EMI risk).
- Other wires spiral around the core to make a layer, then spiral another layer the **opposite direction** of the previous shielded layer.

  > *flexural wires most central*
  >
- Next layer on top of shielded core is **powers and grounds** (not the ignition-system ones as mentioned before as ignition is split off in the harness). Instead, this concerns sensors, pcbs etc. one central power line for all sensors (5V — minimal shielded-cable interference) and ECU grounds.

**3. Grounding**

- All the grounds that matter → **all to one central point**, not just multiple grounds to chassis at different points.
  - Star point, **star burst!**
  - Generally Rob uses back of the engine. ⟵ *clean-ish array at one central position*
    - `BAT(–)  ECU(–)`  *(node is same DBN5[?])*
  - e.g. Dash CPU will ground-run in the harness to the back of engine block.

**4. Assembly tools:** *(⟵ add a few helix[?] of slack)*

- **Zipties** — short zipties — hold things in place / snips as well.
- **Vice** — clamp on the extra inch of conductor then split off the end. *(crushed)*
- **Kapton tape** — heat resistant but lacks elasticity.
- **16 and 22 AWG wires.** Wire cutters / strippers.

**5. Filler wire**

- At a 45° angle in, but if shielded cable still visible… *(margin: use consistency testing to load specific wires[?])*
  - A **pro harness** (!) uses dummy wires / filler wires to fill space.
  - In Rob's case he added extra ground and your[?] wires for extra safety — actually then saw shield wasn't still visible, so added more.
  - Filler wire in blank. *(margin: wrapped as good — more than saving, but good for protection and quality)*
  - Once enough wire to cover surface area of shielded cable, zip the wires to the end, position at 45° and begin wrapping around; hold in place w/ vice at both ends.
- Get wires to twist, not fall on top of each other.

---

## Preparing Wires to Leave Harness

**Engine harness fully-done layers:**

1. Shielded
2. Power lines and ground 12V–5V
3. Sensors from ECU → engine loom
4. ½ Ignition-coil signal and data lines to relay

**6. Preparing wires to leave harness (??? as in, to leave engine harness?), to splice to rest of harness.**

Progress RN: `DASH → ECU —20"→ Splice —now→ Rest of harness → Engine` (Dash)

- If working on separate sections of the firewall individually, harness can get too thick for sheath.
- Make a mark about an inch before where you want the splice off the harness, due to the sheath split.
- Core section of harness: filler wire stops, then wires at that [point].
- At the other end he has **8 × 12V red 16-gauge wire**; then **11 × black sensor grounds** of the main harness via single crimp from main length to be split off through the loom; **7 × red/white 5V sensor power 22AWG**.
- This layer added 5V line — **5-to-1 splice** for 8 wires. *(crimp splice)*
- Heat shrinks on crimp, then **DR25 on top** for strain relief and ingress. 12V line is a **7-to-1** crimp splice. *(crimp)*
- Kapton tape holds this layer together and lets the next layer slide.
- Need to ensure centre section is heat-shrunk before component connectors. *(margin: 6 heatshrink with adhesive at engine ends)*
- Math to calculate based on diameter of core and layer 1 to determine layer 2.
  - Rob takes 25 wires, coloured for specific sensors across the car, and spirals in the opposite direction of the layer below.
  - Layer 2 wires are individual for the engine loom. *(margin: then epoxy for weatherproof, then SCL)*
  - Clutch switch / transmission will be on another entire layer.
  - When reaching splices from layers below, the twist on the Kapton layer should allow splice wires to escape without ingress. *(margin: want it dense — drop of Kapton · RAYCHEM, no adhesive)*
- Once at branching point, left as strands of wires.
- **DR25 has a 2:1 shrink ratio** — so 3/4 shrinks to 3/8.
- Central core between ECU branch and engine firewall is **not heat-shrunk**.

---

## Layer 3, Gluing Points

**6. Layer 3 ½** *(concentric twist means your wire shortens[?] over)*

- 6 × ignition signals to smart coils, 5 × sensors (inc. clutch pedal), 2 × data lines to relays, 1 × spare.
  - Ignition or ground lines, bundled with ECU-side power splice wires (ignition coils can go off on their own).
  - Need to add Kapton tape to layer above, where layer-3 new wires are.
  - Connects onto exit splice, then begins concentric twist opposite direction of layer 2.
  - Adds layer 3 but leaves space for another half of twist — kept open right now, but will have filler wire for pro loom (can get magnetic wire filling[?]).
  - Sometimes need to go back and re-length the layer for extra length to connector, using spare filler as red/white.
- **Filler wire** held in place at ends of loom via Kapton tape — ensures outer layer of epoxy does not stick to wires.
  - Nose-to-nose at core end, then half of Kapton tape at branch end.
- Braided branching wires off the core harness, with 4 extra wires (secured with Kapton, on top of straight power wires).
- Braided yellow injectors around itself, then Kapton to splitting point (connector plenty[?] e.g.).

**7. Gluing / Kaptech[?] points of loom via adhesive heatshrink.**

- Kapton tape (after drying moisture from connecting joint) and onto both (roughly).
- Then Saran[?] paper on both ends of Kaptech at adhesive section.
- For strain relief, zip-tie both ends of adhesive SCL.
- Then the air pocket from branching loom is filled with epoxy glue to fully seal.

---

## Splitting to Engine Loom

**8. Splitting to Engine Loom**

- We do **not** want each branch of wire to go to every single thing from the branch point (currently) — heatshrink is expensive.
- Instead make **stalks / branches** that go from centre area of sected[?] engine (for this specific engine), then to specific parts around after the centre / bourne[?] part of engine (branches out). *(3 NS[?])*
- E.g. **stalk from CRANK SENSOR** — [diagram: Rest of harness — CRANK Sensor (shielded core) → MAP / CAM]
  - Shielded wire, i.e. end of core: `ECU → Firewall → Engine loom`, so stalk then splits to each of the six injectors. Each injector takes **12V, ECU signal and GND**.
- **Firmboard** useful here, so physically separating remaining wires into groups. *(margin: to engine body / against loud[?])*
- When separating, ensure wire can go back as free to common point as possible — **no knots wanted**.
  - Rob likes GND flexibly — sensor GND in middle of harness as needed by eng[ine] sensor. He is physically picky about which wires best suit their future loom position.
  - Goes by each component and their required wires.
  - Then sees spaces left — spares run along through part. *(margin: concentric twist w/ filler wire along shielded core)*
- After separating, create stalks — stalks are branched, no centres.
- More Kapton tape.
- The branch region: non-sticky Raytech between them, then the sticky stuff over all 3 separate sections. Then tape over, then the SCL. *(raysclontop[?])*

---

## Labelling & ECU-Side Pinning

**9. Labelling parts of harness**

- Used ball marker, then heatshrink, then clear heatshrink on top of that. (welp that's quite a bit of heat shrink)
- Keep name free.

**10. ECU-side pinning** *(cabin / cockpit side)*

- Other end of Crank Angle Sensor (shielded cable).
  - Ensure shield is grounded to engine chassis, **not** to sensor GND.
- Continuity test 1-by-1 to decide which wires are spare / required.
- On ECU end, important to deal with the shielded crank-angle-sensor:
  - Bring it back significantly; wire must go hard-ish[?] to cut.
  - Grab just the sheath → tautly back to ground, but to engine side of power.
  - To cut shield braids, untwist / snake the wire from root of un-scathing[?] point, so the in-twisted parts of wire (signal) are undamaged and unscathed from shield braid at the ECU end.
  - Sometimes go to sensor GND; Fuel Tech goes to specific pinout.
  - **READ ECU DOCUMENTATION!**
  - The shield part of the wire is now to be crimped and grounded out → Rob crimped shield stalk, and the other ground wire is a **2-out crimp**. *(margin: post crimp uses [tool] from side to crimp — faces red[?] of sharp edges)*
  - Grounds now provide for crank-angle sensor also. *(margin: strongest part of harness, as centre of harness is saturated with twisting)*
- Super-seal connectors for ECU; pins and service loop at joint on harness before ECU connector — strain relief. *(margin: he used a crimp tool, no time[?])*
- ECU pins, for conductor and the resistance, plus inspection holes.
  - Start with bigger wire gauges in ECU first.
- [crossed out] Make sure correct pinouts — namely INJ1, INJ2, IGNI1, IGNI2.

---

## Booting, Epoxy, Cost

**11. Booting connectors**

- Can use filler heat-shrink under adhesive boot heatshrink to ensure boot fits, and buffers to adhere to connector shape. Kapton to protect wire from adhesive.

**12. Epoxy gun** — *3 different styles:*

- Epoxy on connector, from harness to connector heatshrink.
- Epoxy on connection-side [above wire] moulded boot.
- Epoxy on non-adhesive heat-shrink to non-adhesive heatshrink to connector; then epoxy around connector and new heatshrink; then heat-shrink adhesive boot on top (water not sendable[?] / airtight[?]).
  > *cheaper than full pre-moulded boots · use Tefzel · not fully milspec*
  >
- Oil and fuel sensors most important, as in contact with most potential ingress — uses this technique. **Do not boot the CKP!**
- Needs to dry afterwards.

**13. Cost** *(core-of-milspec items ↑ / not-fully-milspec ↓)* 

- Costs more to make harness first time around:
  - $16,000–18,000 (4 years ago, so 2022)
  - Tefzel wiring — $300
  - DR25 — $500 (enough left for 2 additional harnesses)
  - Connectors — couple hundred bucks
  - Boots — $7 per boot
  - Epoxy + labels etc. — a lot; at least a couple hundred
- Cheaper than aerospurts[?] and sub-harness development.
- Milspec vs old harness ⟵ crimped old stock to new exposed; 3M boot shown, exposed wire next to it.

> **Never pull on crimped wires already terminated in a connector. — Rob's pet peeve.**
