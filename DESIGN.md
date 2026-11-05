# Well-water design — approved cuts + spec-review fixes (rev. closet-v6 open bay)

Site: private well · 1" main · existing pressure tank.

## Closet geometry (closet-v6)
Open bay: **BACK wall 72″ + LEFT wall 40″ deep**, height 106″. **No right wall, no front wall/door.** Pressure tank back-left; 3″ floor drain back-right against the back wall at the open end. Wall-mounted train, bypass, outlets, and NEMA on the **back or left wall only**. Floor tanks (AIO, softener, brine) serviceable from the open front. NEMA on the back wall near the open right (~80″ AFF); door hinged left, opens toward open right.

## Treatment train
Well → existing pressure tank → **P0** → **Rusco 1-140-F 1" spin-down filter (140 mesh ≈ 104 µm) + Rusco AFV timed automatic flush valve** → DAE MJP-100P pulse meter → **leak shutoff: GC Valves NS201YH16C7FG9 1" 316SS zero-differential NC solenoid (spring-return, fail-closed)** → **AIO air-injection iron filter (Clack WS1, Katalox Light)** → **P1** → AquaHome Clack WS1 64K softener (12x48, 2.0 ft³) + EZsalt → **P2** → Big Blue 20" 5 µm → **P3** → **6 gpm limiter (neoFlo FRSS-6-100FF)** → VIQUA PRO20 UV (bundled restrictor NOT installed) + COMMcenter → **UV shutoff: GC NS201YH16C7FG9 1" NC solenoid (spring-return, fail-closed)** → **P4** → house. Kitchen: **Delta Clarifi DWQ1001012 tankless RO** (NSF/ANSI 58/53/401 certified, IAPMO) + DWQ300300 remineralizer + DWQ4001002-SS air-gap faucet (replaces Frizzlife PD600-TAM3, which had no NSF/WQA listing).

## Approved cuts
1. **Continuous chlorination removed.** That means the Stenner pump, contact tanks and Hach CL17sc are gone. Instead there is a one-time shock chlorination at install (see INSTALL_NOTES). UV is the only continuous disinfection.
2. **Catalytic carbon tank removed**, together with its bypass. It was only needed to remove chlorine residual.
3. **Filter-Ag Plus replaced by an AIO air-injection filter** (Aquatell Atmos-AIO, Clack WS1, 10×54). **No backwash booster.** The AIO backwashes at about 6.5 gpm, so the well must sustain **≥6.5 gpm at ≥40 psi** for the backwash duration. Verify this with a flow test **at the AIO inlet, after drawing the pressure tank down** (so the number is pump yield, not tank storage) before ordering. If the well falls short, choose a 9" tank or a lower-rate media rather than adding a booster.
4. **Pressure taps cut from 12 to 5:** P0 well/pre-iron, P1 post-iron, P2 post-softener, P3 post-5 µm/pre-UV, P4 post-UV.
   - Each tap is a 1" tee + 1×¼ bushing + ¼ mini ball valve + 0.5–4.5 V transducer.
   - Gauges at P0 and P4 only.
   - **P3 is the justified extra.** P2→P3 gives the cartridge ΔP, which is the clog alarm. P3→P4 spans the **6 gpm limiter + UV + UV shutoff valve** (the limiter sits between P3 and the UV), so the P3→P4 baseline includes the limiter drop; a stuck or partly closed valve shows as a rise above that baseline, separately from a plugged cartridge.
5. **Whole-train main bypass (rev 2026-11-05) + per-component isolation.** A 1" full-port bypass runs from a tee just after the existing pressure tank (before P0) to a tee on the house side after P4. Three valves: the first component's inlet isolation doubles as **main inlet isolation**, the last component's outlet isolation doubles as **main outlet isolation**, and a **lockable main-bypass valve** sits on the bypass loop (normally padlocked CLOSED). A reed switch proves the main bypass is closed; if open/unknown, HA raises a persistent **"UNTREATED WATER — MAIN BYPASS OPEN"** alert and a phone push. Opening the main bypass also bypasses the leak shutoff solenoid — treated as intentional. Each component in the train (spin-down, pulse meter, leak solenoid, AIO, softener, Big Blue, flow limiter, UV, UV solenoid) has its own inlet/outlet 1" full-port ball valves plus brass unions for service. When a component's isolation would cut house water, open the main bypass first. Clack WS1 heads on the AIO and softener typically include a Clack 1" bypass valve — **confirm included with Aquatell/AquaHome orders**. UV lamp/sleeve service uses the UV and UV-solenoid isolation valves (main bypass covers house water). See Open decision below on padlocks.

## Power (new fact: solar + whole-home battery, seamless switchover)
- **No UPS and no mains-sensing outage relay.** The house battery keeps the UV, the COMMcenter, HA Green, the ESP32 and both DIN supplies powered through outages.
- The valves fail safe on their own. Each GC NS201 is an energize-to-open NC solenoid whose **mechanical spring** closes it on a UV fault/alarm, a leak trip, or loss of 24 V.
- **Valve decision (rev d):** both shutoffs are **GC Valves NS201YH16C7FG9**: 1" FNPT, 316 SS body, EPDM, NC, **0 psi minimum operating differential** (GC NSF spec sheet + AutomationDirect cut sheet), "single solenoid spring return" with a spring-loaded plunger, NSF/ANSI/CAN 61, 24 VDC 10 W, Cv 11 (≈0.3 psi drop at 6 gpm), **100 psi max**. Keep the tank relief valve at ≤100 psi. It costs $611 each and AutomationDirect shows 7 available, with free 2-day shipping. The NS711YH16C9FG9 ($306) is the fallback only; GC's sheet lists an **8 psi** minimum differential for it. The USS-MSV40064 was rejected because U.S. Solid documents its auto-return as capacitor-based. Valworx Surpass is also super-capacitor and ships in 2–3 weeks. Belimo B2+LF24 is not NSF 61.

## Interlocks and controls
- **UV interlock:** VIQUA COMMcenter 270272-R. Its 260201-R dry contact (red/black) is **closed only while the UV is healthy** and opens on alarm or loss of UV power.
  - The contact switches the 24 V coil of the AutomationDirect ZL-RLS1-24 interposing relay. The relay's NO contact powers the UV shutoff valve.
  - Never run valve current through the COMMcenter contact.
  - Contact rating of the 260201-R is **not published** (manual only says "stay within contact ratings"). Request it from VIQUA tech support before energizing; the relay coil load is small, but confirm it.
  - 1N4007 flyback diodes across the relay coil and both solenoid coils.
- **Leak shutoff:** a second GC NS201, switched from 24 VDC through a Shelly 1 Gen4 UL dry contact. **The Shelly is powered from 120 VAC** (L/N), power-on default = **restore last**.
  - A **direct Shelly Flood → Shelly 1 OFF action** (Shelly local actions/scenes) closes the valve even if HA is down; HA leak logic (pulse meter plus Flood) is a second path.
- **Valve-position feedback and alarms:** the solenoids have no limit switch, so HA infers position. Alarm on mismatch: (a) leak valve commanded closed but DAE meter pulses continue; (b) UV valve commanded closed but P4 holds/flow continues, or commanded open with P3→P4 ΔP above baseline. **Monthly close test** (HA automation, on a hose bib draw): command each valve closed in turn, confirm zero meter pulses / P4 decay within 30 s, reopen, log pass/fail.
- **Power rails:**
  - Mean Well HDR-60-24 feeds the 2 solenoids (10 W each, continuous) and the relay coil.
  - **Mean Well HDR-15-5 (fused) is the protected 5 V rail** for the 5 transducers **and the ESP32 (5V pin, not USB)**.
  - HA Green runs from its **included 12 V 1 A adapter**, not USB-C.
- **Pressure signals:** 5 × Honeywell **MIPAN1XX100PSAAX**, 0–100 psi sealed gauge, 0.5–4.5 V ratiometric, **1/4 NPT**, 5 V. (DATAQ 2000500-100H, now $79, is the fallback.)
  - The ADS1115 runs at 3.3 V. Each signal goes through a **4.7 k / 10 k divider** (4.5 V → 3.06 V), so the inputs never exceed the ADC rail.
- **Other monitoring:**
  - The UV 4-20 mA intensity signal (270268-R) goes to the NOYITO converter **set to 0–3.3 V output**, through a 1 k series resistor so the ADS1115 input diodes clamp at 3.3 V. If the 270268-R sources loop current itself, drop the NOYITO and use a **150 Ω shunt** (20 mA → 3.0 V).
  - Brine salt level: **EZsalt sensor** bundled with the AquaHome softener (ESPHome, local). The DIY VL53L0X is removed.
  - Shelly Plug on the UV.
  - The **main-bypass** reed switch drives the persistent HA alert ("UNTREATED WATER — MAIN BYPASS OPEN").

## Pre-order go/no-go (all must pass before ordering)
1. Certified lab water test (Fe, Mn, H₂S, hardness, pH, TDS, turbidity, **UV transmittance (UVT, %T at 254 nm)**, **tannins**, coliform; plus As (speciated III/V), nitrate/nitrite, uranium/gross alpha, Cr6, F). PRO20 needs UVT >75% and tannins <0.1 ppm; nothing in the train treats tannins. Results must land within the PRO20 feed limits after treatment. **Size the softener on post-AIO hardness** (Katalox/calcite/Corosex in the AIO raises hardness), not raw hardness.
2. **Well-yield test ≥6.5 gpm sustained at ≥40 psi through the real path** (the AIO backwash rate), **measured at the AIO inlet after the pressure tank is drawn down**.
3. **One restrictor only.** The PRO20 ships with its own flow restrictor; do not install it. The neoFlo 6 gpm limiter is the single restrictor (sized to the well and AIO, not the 20 gpm UV).
4. **Aquatell written rating** for the Atmos-AIO at the planned service flow. The AIO is rated 8 gpm; the 6 gpm limiter is the default and the 8 gpm FRSS-8-100FF is allowed only if this rating and the well test support it.
5. RO = Delta Clarifi (certified); no manufacturer letter needed. Feed 20–80 psi (OK on 40/60 or 50/70).

## Model
`water_system.html` and `water_system_offline.html` (and `index.html`) have been updated to match. The model reads its geometry from the `<script id="model-data">` JSON, so the offline bundle's JS was unchanged and **no esbuild rebuild was needed**. The model has 228 objects (COMMcenter and relay/DIN boxes added; NC spring-return solenoid valves; limiter 6 gpm; UPS removed), and it rendered successfully in headless Chrome.

## Budget
**Rev g online total (order/gen.py): $11,902.83, no holds (owner: buy everything now).** Rev f was $12,458.22 incl. the Resideo hold. Softener now 64K $1,799.00; RO now Delta Clarifi $799 + remineralizer $69.90 + faucet $159.90 at Ferguson Home. Older figures below are history.

See BOM.csv. **Equipment ≈ $11,207** (rev d; was $10,597 rev c, $11,038 rev b): AquaHome PRO20 $3,264 (Walmart/ESP fallback $3,465.28), AquaHome WS1 48K + EZsalt ≈$1,335.51 (both sale prices to confirm at checkout), 2 × GC NS201 $612 (was $487.98), 5 × Honeywell $72.77 (the ~$42.23 snippet did not hold), VL53L0X removed, 4 × 1N4007 added, 3rd coliform test added. **≈ $10,338** with the LWS PRO20 ($2,394.95, delivery unverified). The resistor kit is still unpriced. **Installed estimate: ≈ $14,200–17,700** (AquaHome UV) / ≈ $13,300–16,800 (LWS UV), incl. labor ≈$2,500–5,000 and misc ≈$500–1,500.

## Acceptance gates
- Flow test ≥6.5 gpm sustained at the AIO inlet (after tank drawdown) before ordering the AIO.
- Iron/Mn/H₂S/hardness lab results confirm AIO media sizing.
- Two coliform-negative results (Tap Score ×2) after shock chlorination before handover.
- Interlock tests pass (see INSTALL_NOTES commissioning), including the monthly close test baseline.
- **Yearly:** sanitize the AIO (Clack/Aquatell procedure) and run a coliform test (Tap Score #3 or OK DEQ).

## Rev e (SUPERSEDED by rev g — kept for history): sediment pre-filter = Resideo F76S1023 + MV876B1018
Same location (after the pressure tank and P0, before the meter). Vetted against Resideo 33-00557 (installation instructions) and 67-7469 (spec sheet):
- **Flow:** Cv 18 → ≈0.2 psi at 8 gpm and ≈0.13 psi at the AIO's 6.5 gpm backwash; Resideo sizes for ≤3 psi (31 gpm on 1"). The F76S keeps supplying filtered water through its upper screen during its own backwash.
- **Pressure/temperature:** min 22 psi inlet with an unrestricted backwash outlet; max 232 psi (plastic sump), 104 °F. Fine on a 40/60 well switch.
- **Backwash:** ~20 s, ≈4 gal per 15 s at 60 psi (≈16 gpm burst) → short oversized unrestricted drain to an air gap; don't raise the outlet. Do not run it during an AIO regeneration (schedule the MV876B / HA trigger away from the AIO's night regen); the pressure tank covers the burst.
- **Iron:** raw-water iron is mostly dissolved and passes the 100 µm screen to the AIO. Oxidised flakes, iron bacteria and sand are caught and backwashed. Rust staining of the clear sump and slow fouling of the SS screen are expected; frequent (weekly or faster) backwash plus a yearly look keeps it clean. It is not an iron remover.
- **Approvals:** EU DVGW/SVGW for the 100 µm versions. **Lead-free (SDWA/NSF 372) and NSF 61 are NOT stated in Resideo's U.S. literature** → get written confirmation from Resideo before buying. If they can't confirm, use the fallback: Rusco 1-100-F + AFV.
- **SKU:** F76S1023 is the U.S. 1" model (NPT/sweat union tailpieces, gauge included). The "-1AA"-style F76S part numbers are EU BSP versions; don't substitute. Keep the stock 100 µm screen (finer than the Rusco's 100 mesh ≈152 µm); AF11DS-1A is the 1–1¼" replacement/spare screen.
- **Mounting:** horizontal pipe, sump down, indoors out of sunlight; ≈24 in clear below the pipe centreline.
- **HA:** MV876B (24 VAC, 4 VA) runs one backwash at every power-up, so a Shelly 1 Gen4 switching its 24 VAC lets HA trigger it. Its own timer stays as a backup. A "remote activation" input is advertised but not documented in the U.S. manual (verify on site). There's no feedback output, so HA infers a backwash from the P0 dip.
- **24 VAC:** a dedicated Robertshaw 620-202 plug-in (20 VA) for the MV876B. The OpenSprinkler keeps its own bundled 24 VAC adapter. Reasons: OpenSprinkler valve inrush and grounding stay isolated; the MV876B supply has to be switched by HA independently anyway; the OpenSprinkler isn't purchased yet. It fits on the enclosure outlet strip (20×16×8 in box).
- U.S. stock: SupplyHouse F76S1023 $588.86 (17 available), MV876B1018 $345.39 (19 available).

## Drains (WW-DRAIN3-v1, 2026-11-04)
- **Collection point:** all treatment drains go to the **existing 3″ drain at the BACK-RIGHT end of the back wall** (open right end; no right wall), through one **3" standpipe/receptor with a P-trap per code** (rim 18–42" above the weir; vent per code). **Gravity drain lines (brine overflow, AFV flush after the air gap, and any open drain) must fall continuously (≈¼"/ft) to their own air gap above the receptor — no risers or high loops.** Pressurized Clack backwash/regen drains may be rigid and pitched downhill to the same receptor.
- **Air gaps:** each line ends in its **own clipped, visible air gap ≥ 2× its diameter**.
- **Routing:** lines run right along the wall, sloped. Nothing is teed together.
  - **Brine overflow** is gravity: continuous fall, never teed into a pressurised line.
- **F76S drain:** it sits at the far left, so the run is ≈17 ft, too long for Resideo's "short, oversized, unrestricted, not raised" drain requirement. Fix: a local air gap right under the MV876B, then a 2" DWV gravity line at ¼"/ft (≈ 4¼" fall), which ends ≥ 4" above the receptor rim.
  - Check on site that the outlet height leaves room for that fall. If it doesn't, move the receptor closer or use 3" at ⅛"/ft.
- **Regen/flush schedule (staggered):** AIO 2 AM, softener 3 AM, Rusco AFV on its own timer set to an afternoon start. Staggering protects the well's flow and pressure budget, not the drain.
- **RO reject:** stays at the kitchen sink drain, because the RO is a kitchen point-of-use unit.
- **Pressure-tank relief discharge:** per code (TBD).


## Rev f (2026-11-04): worst-case sizing — Delta Clarifi RO + 64K softener
- **Softener:** AquaHome Clack WS1 **64K, 12x48, 2.0 ft³** resin, 18x33 brine tank, EZsalt ($1,799.00). Sized for a bad-case central-OK well (15–30 gpg + residual Fe; the AIO's calcite/Corosex adds hardness). ~10K grains/day at 30 gpg × 300 gal/day → regen ≈ every 4–5 days at efficient salting (vs 2–3 days on the 48K). **Backwash ≈ 3.5 gpm** (Clack standard DLFC for a 12" tank; confirm the DLFC on the delivered valve) — well below the AIO's 6.5 gpm, so the AIO stays the governing backwash. Footprint: 12" Ø × ~55" with valve; leave ≥ 12" above the valve for service.
- **RO:** Delta Clarifi DWQ1001012 (600 GPD, 2:1, tankless, 120 V, 3/8" feed, 20–80 psi). IAPMO-certified NSF/ANSI 42/53/58/401/372 + ASSE 1086. PDS: As(V) 0.30→0.002 mg/L, nitrate 27→0.7 mg/L, Cr6 0.3→0.004, Cr3, Pb, Ba, Cd, PFAS. **Limits:** As claim is pentavalent only (AIO air-oxidation upstream converts As(III); verify by speciation); nitrate claim only to 27 mg/L influent; uranium and radium not certified. + DWQ300300 remineralizer (inline, 24 mo) + DWQ4001002-SS faucet (Clarifi ships without a faucet; integrated air gap).
- **Post-install RO-output test (required):** ~2 weeks after start-up, one lab panel on the RO faucet: arsenic (total + speciation of the raw tap), nitrate/nitrite, uranium + gross alpha, Cr6, fluoride, lead, TDS. If raw nitrate > 27 mg/L as N, or raw U > 30 µg/L, test RO output quarterly for the first year.

## Rev g (2026-11-04, owner decision): sediment pre-filter = Rusco 1-140-F + AFV
- **Replaces** the Resideo F76S1023 + MV876B1018, its Robertshaw 620-202 24 VAC transformer and the 2nd Shelly 1 Gen4 (they served only the MV876B; nothing else uses them). Same spot: after the pressure tank and P0, before the meter.
- **Rusco 1-140-F:** 1" PVC socket (slip) body, 140-mesh polyester screen (≈104 µm), clear sump, 1–25 gpm, 150 psi, max 75 °F water, 11-3/8" × 5". Not NSF/ANSI 61/372 listed (as before with the F76S, accepted by the owner). Spare screen FS1-140 on the shelf.
- **Rusco AFV:** threads onto the filter's 1/2" flush port; built-in timer 1 min–14 days; each cycle opens a full-port ball valve for ~3.5 s (≈0.9 gal at 30 psi). 120 V, 2.5 A, 8 ft cord, NEMA 4.
- **Control decision (simplest):** the AFV runs on **its own timer, plugged into a plain receptacle — no Shelly, no HA power-cycling.** Start at once every 3 days, afternoon start; adjust from how fast the sump loads. HA can see each flush as a short P0/meter blip if wanted. (Optional later: a Shelly Plug could monitor/cut its power, but it is not needed and not bought.)
- **Drain:** the burst is small (≈0.9 gal), so the long 2" gravity line is no longer needed; a 1" PVC line sloped to the receptor, ending in its own air gap, is enough.
- **No holds:** owner instructed buy everything now (overrides audit holds). Lab-dependent items are sized for a bad-case well (rev f).


## Rev 2026-11-05 — whole-train main bypass + per-component isolation
GC requested a full bypass so the house stays on during service. Approved and incorporated:

1. **Main bypass loop** (tee after pressure tank / before P0 → tee after P4 / house side) with inlet ISO, outlet ISO (shared with first/last component outer valves), and a lockable 1" full-port bypass valve (normally padlocked CLOSED + reed switch → HA persistent alert + phone push). Opening it also bypasses the leak shutoff.
2. **Per-component isolation:** inlet/outlet 1" full-port ball valves + brass unions on spin-down, pulse meter, leak solenoid, AIO, softener, Big Blue 5 µm, flow limiter, UV, UV solenoid. Clack bypass valves on AIO/softener — confirm with Aquatell/AquaHome. Main bypass covers house water whenever a component is isolated.
3. **P0–P4** positions unchanged. Sampling ports S0–S3 kept.
4. Schematic: `bypass_diagram.png` / `.svg`.

### Open decision — padlocks (was: only ONE padlock, on the UV bypass)
Previously the design had a single padlock on a UV-only bypass. The main bypass also needs a lock (untreated water to the whole house is a bigger risk than UV-only bypass). Options:
- **(A) Recommended:** one padlock on the **main bypass** only. Drop the separate UV bypass valve; UV service uses UV + UV-solenoid isolation valves with the main bypass open for house water. Keeps the single-padlock intent.
- **(B)** Keyed-alike pair: one padlock on the main bypass and one on a retained UV bypass (same key). Two physical locks, one key.
- **(C)** One padlock on UV bypass only (rejects the GC request — not recommended).

**Recommendation: (A).** Docs/BOM currently assume (A): the Raven lockable valve and single padlock move to the main bypass; no second reed; UV keeps plain isolation valves only.


## Closet envelope (rev 2026-11-05)
Treatment closet interior: **72" wide × 40" deep × 106" high**. Door left/front; pressure tank stays back-left; 3" drain BACK-RIGHT; stubs low on right wall; outlets on back wall. Layout drawings: `closet_plan.png`, `closet_elev_back.png`, `closet_elev_right.png`. Fit table: `CLOSET_FIT.md`. Kitchen RO is not in this closet. Service aisle is tight (~18–22"); UV lamp-pull fits if reactor base ≤~30" AFF.
