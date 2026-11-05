# Plumber / electrician notes (rev. 2026-11-05 — whole-train main bypass + per-component isolation)

## Plumber — order of work
1. Run the flow test **at the AIO inlet, after drawing the pressure tank down** to pump cut-in (so you measure well yield, not tank storage). The AIO backwash requires ≥6.5 gpm sustained at ≥40 psi. **There is no booster pump.**
2. Install the train in this order: tank → P0 → **Rusco 1-140-F spin-down filter + AFV** → meter → leak shutoff → AIO → P1 → softener → P2 → 5 µm → P3 → 6 gpm limiter → UV → NC spring-return UV solenoid → P4. Note the limiter sits between P3 and the UV, so P3–P4 includes the limiter drop. Do **not** install the PRO20's bundled restrictor — one restrictor only (neoFlo 6 gpm). Observe flow arrows on both GC solenoids → house.
3. Fittings: 1" lead-free brass unions on each side of every component, 18 × 1" full-port isolation ball valves (2 per component × 9), plus 1 lockable 1" full-port on the main bypass, and 4 sample taps (raw, post-iron, post-softener, post-UV). Preferred jointing: PEX-A expansion or soldered/press copper. **No push-fit fittings.** Mount the UV vertically.
4. **Whole-train main bypass:** tee just after the pressure tank (before P0) to a tee on the house side after P4. The spin-down inlet isolation doubles as main inlet isolation; the UV-solenoid outlet isolation doubles as main outlet isolation; the **lockable bypass valve** on the loop is normally **padlocked CLOSED**. Mount the reed switch and magnet on its handle so "closed" = contact made. HA raises a persistent **"UNTREATED WATER — MAIN BYPASS OPEN"** alert + phone push while open/unknown. Opening the main bypass also bypasses the leak shutoff — intentional. See DESIGN.md Open decision: recommended single padlock is on this main bypass (UV service uses component isolation; no separate UV bypass valve).
5. Taps P0–P4 and sample taps S0–S3 each use a 1" tee → 1×¼ bushing → ¼ mini ball valve (9 of each). At P0 and P4, a ¼ brass tee carries both the gauge and the transducer. The Rusco 1-140-F has **1" PVC socket (slip) ports**: solvent-weld 1" Sch 40 PVC male adapters (MPT) and go into lead-free brass unions on each side.
6. **Rusco 1-140-F + AFV (sediment pre-filter):**
   - Horizontal pipe run, flow arrow toward the meter, **sump hanging straight down**, unions both sides. Leave **≈ 18 in clear below the pipe centreline** for the sump (≈ 11-3/8 in) and the AFV, plus room to unscrew the clear cover by hand (no tools). Indoors, no sunlight, cold water only (max 75 °F, 150 psi). Support the pipe on both sides — the PVC body must not carry the brass.
   - Remove the filter's manual 1/2" flush valve and thread the **AFV** onto the 1/2" port (PTFE tape). Plug the AFV into its own 120 V receptacle (no relay, no Shelly). Set its timer: start once every 3 days, afternoon.
   - **Flush drain:** each cycle is ≈0.9 gal in 3.5 s. Run 1" PVC from the AFV outlet, sloped to the 3" receptor, ending in its own air gap. Do not add any valve on the drain.
7. **Drains: everything goes to the EXISTING 3″ drain at the BACK-RIGHT end of the back wall** (open right end; no right wall).
   - Install a **3" standpipe with a receptor funnel and a P-trap per code**: rim 18–42" above the trap weir, vent per local code.
   - **Gravity drain lines** (brine overflow, AFV flush after any local air gap, and any open drain) must run **continuously downhill (≈¼"/ft)** to their air gaps over the receptor — **no risers, no high loops**. Prefer the same continuous downhill pitch for Clack pressurized backwash/regen lines (rigid only if rated for an overhead route; otherwise keep them simple downhill).
   - End each line in its **own visible air gap ≥ 2× its diameter, clipped just above the rim**:
     - Rusco AFV flush: 1" line, ≈0.9 gal bursts (see 6).
     - Atmos-AIO backwash, ~6.5 gpm: dedicated pressurised line (prefer downhill).
     - Softener regeneration drain: dedicated pressurised line (prefer downhill).
     - **Brine overflow: gravity only, continuous fall the whole way, NEVER teed into a pressurised drain line.**
   - No tees between lines.
   - The RO reject stays at the kitchen sink drain (via the DWQ4001002-SS faucet air gap, 3/8" drain tube to a drain saddle above the trap), because the RO (Delta Clarifi, under the kitchen sink) is not in this space. Route the pressure-tank relief discharge per code (TBD).
   - HA staggers the backwashes (AIO 2 AM, softener 3 AM, Rusco AFV afternoon on its own timer) even though the 3" drain could take an overlap.
   - No chemical lines (chlorination removed).



## Closet layout (72" W × 40" D × 106" H) — rev closet-v6 open bay
**Walls: BACK (72″) + LEFT (40″) only. Front and right are OPEN** (no door, no right wall). Existing **pressure tank stays back-left**. **3″ drain** standpipe is **BACK-RIGHT** at the open right end of the back wall (floor, against the back wall). Outlets/conduit on the **back or left wall only**. Carts/ladder/hose leave. Kitchen RO stays under the kitchen sink.

Suggested placement (see `closet_plan.png`, `closet_elev_back.png`, `closet_elev_left.png`, `CLOSET_FIT.md`):
- **Floor (service from open front):** pressure tank (back-left) → AIO 10×54 → softener 12×48 along the back; **brine 18×33** forward of the softener toward the open front.
- **LEFT wall (wall-mounted train ≈ 48″ AFF):** stubs → spin-down+AFV → meter → leak solenoid → (front-aisle jump to AIO/soft) → return → Big Blue → 6 gpm limiter → PRO20 UV (vertical) → UV solenoid → house.
- **Main bypass** high (~96″ AFF) on the LEFT wall, single padlock CLOSED + reed switch.
- **NEMA 20×16×8 + HA Green** flat on the **BACK wall near the open right**, ~70–90″ AFF; door hinged on its left edge, swings toward OPEN right (rendered open). Clear of drain air gaps and the bypass. (Left-wall mount was considered; back-near-right is better — keeps the train clear and the door opens into open space.)
- **All drains** short/downhill to the BACK-RIGHT 3″ receptor with individual air gaps.
- UV: mount so lamp/sleeve pull **up ≥36″** still clears the 106″ ceiling (base ≈28–30″ AFF for a ~40″ body).
- Prefer PEX-A expansion or soldered/press copper; brass unions; full-port ball valves; **no push-fit fittings**.

## Per-component isolation and service
Each of the following gets an inlet and an outlet 1" full-port ball valve plus a brass union on each side (valve → union → component → union → valve): Rusco spin-down + AFV, pulse meter, leak shutoff solenoid, AIO iron filter, softener, Big Blue 5 µm housing, flow limiter, UV, UV solenoid. Clack WS1 heads on the AIO and softener typically include a Clack 1" bypass — **confirm included with Aquatell/AquaHome orders**. To service any one component without cutting house water: open and unlock the main bypass, close that component's inlet and outlet isolation valves, then break the unions. Relock the main bypass before leaving the job. Pressure taps P0–P4 stay in their existing positions; sample taps S0–S3 optional but recommended (raw, post-iron, post-softener, post-UV).

## One-time shock chlorination (replaces continuous chlorine)
1. Install everything except the UV lamp and the 5 µm cartridge. Put the AIO and softener in bypass. **Isolate the RO** (close its feed valve). **Unlock and open the padlocked MAIN bypass** so chlorinated water reaches the house lines (HA will show the MAIN BYPASS OPEN alert — expected). Component isolation valves stay open for this step.
2. Dose the well with the NSF-60 kit (Well Safe) per its label for the well depth and casing, targeting 50–200 ppm free chlorine. Recirculate through a hose to the casing until strips read strong.
3. Open each fixture until chlorine is smelled, then let it hold for 12–24 h.
4. Flush to waste, away from the septic field, until the strip reads <1 ppm.
5. Take the treatment units out of bypass, run the initial AIO and softener backwash, and install the cartridge and lamp. **Close and re-lock the MAIN bypass and confirm the reed switch reads CLOSED in HA** (alert clears). Flush the RO feed line, then reopen the RO.
6. After 7–10 days, send coliform/E. coli samples from the raw and post-UV taps (Tap Score or OK DEQ). Hand over only after **two** negative results: kit #1 at 7–10 days, kit #2 on a repeat sample about 1 week later.

## Electrician
- Provide 120 V for the AIO, softener, UV, RO and the controls enclosure from house circuits. The house is on solar plus a whole-home battery. **No UPS.**
- DIN enclosure contents:
  - HDR-60-24 (24 V, for the valves and relay);
  - HDR-15-5 (5 V, fused, for the transducers **and the ESP32 5V pin** — not USB);
  - ZL-RLS1-24;
  - Shelly 1 Gen4 UL (**powered from 120 VAC** L/N; its dry contact switches 24 VDC to the leak valve; power-on default **restore last**);
  - ESP32 + 2 × ADS1115 at 3.3 V, with 4.7 k/10 k dividers on each 0.5–4.5 V input. UV 4-20 mA: NOYITO set to **0–3.3 V out** + 1 k series resistor (clamp), or a **150 Ω shunt** if the 270268-R sources the loop.
- **UV valve wiring:** 24 V+ → COMMcenter 260201-R contact (red/black, closed = healthy) → ZL-RLS1-24 coil. The relay's NO contact feeds the UV GC NS201 solenoid coil. **1N4007 across the relay coil and across each solenoid coil** (band to +). Get the 260201-R contact rating from VIQUA before energizing. Position is inferred (no limit switch): see feedback alarms.
- **Leak valve wiring:** 24 V+ → Shelly 1 Gen4 contact → leak GC NS201 solenoid (1N4007 across coil). The Shelly is normally ON. Configure a **direct Shelly Flood → Shelly 1 OFF action** (works without HA); HA also turns it OFF on meter-based leak logic.
- HA Green runs on its included 12 V 1 A adapter.
- **Sediment flush power:** the Rusco AFV plugs into its own 120 V receptacle and runs on its built-in timer. No 24 VAC transformer, no Shelly, no HA trigger (rev g).

## Commissioning
- Verify all 5 tap readings at no flow: ΔP should be about 0.
- Open a 6 gpm draw. Record the P1–P0, P2–P1, P3–P2 and P4–P3 drops as baselines.
- Pull the UV power, then separately force a UV alarm (COMMcenter test). In both cases the UV valve must close and HA must alert.
- Pull the 24 V supply and confirm both valves spring closed (meter stops, P4 decays).
- Valve-position mismatch alarms: commanded-closed + meter pulses / P4 holding → alarm; commanded-open + P3–P4 ΔP above baseline → alarm. Test each by simulation.
- Set up the **monthly close test** automation (close each valve on a hose-bib draw, confirm zero flow within 30 s, reopen, log).
- Power-cycle the Shelly 1 and confirm it restores ON.
- Rusco: open the AFV manual/test cycle and confirm one ≈3.5 s flush to the air gap (P0 dips briefly). Set the timer to every 3 days.
- Crack the main bypass and confirm the "UNTREATED WATER — MAIN BYPASS OPEN" alert, then re-lock it.
- Wet a flood sensor with HA stopped and confirm the leak shutoff closes via the direct Shelly action; repeat with HA running.

## Yearly
- Sanitize the AIO (Clack/Aquatell procedure), then run a coliform/E. coli test (Tap Score #3 or OK DEQ).

## Rev f additions
- **Softener is 12x48 (64K)**, not 10x54: 12" Ø tank + 18x33 brine tank; leave ≥ 12" above the Clack valve and front access. Drain line per Clack (12" DLFC ≈ 3.5 gpm).
- **Kitchen RO (Delta Clarifi DWQ1001012) under the kitchen sink:** 3/8" cold feed with its own lead-free stop valve (after the UV, softened water); 120 V receptacle in the sink base (GFCI); mount DWQ300300 remineralizer inline on the product line before the faucet; DWQ4001002-SS faucet in a 1-1/4"–1-1/2" deck hole; air-gap drain to a drain saddle above the P-trap. Flush per Delta manual before use.
- **Lab checklist before start-up:** UVT and tannins included (PRO20 limits UVT >75%, tannins <0.1 ppm).
- **Post-install RO-output test:** ~2 weeks after start-up, sample the RO faucet for As, nitrate/nitrite, U + gross alpha, Cr6, F, Pb, TDS.
