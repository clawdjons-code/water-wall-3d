# Closet fit check — 72"W × 40"D × 106"H (rev closet-v6 · open bay)

**Walls:** BACK (72″ along the long side) + LEFT (40″ deep) only. **Front and right are OPEN** (no door, no right wall). Ghost floor outline 72×40; open sides labeled `OPEN (no wall)`.

Photo match: pressure tank back-left; 3″ floor drain at the **back-right end of the back wall** (floor, against the back wall, at the open right end).

| Item | Footprint | Location | Clearance |
|---|---|---|---|
| Pressure tank (exist.) | ~20″Ø × ~60″H | Back-left corner (clears left-wall train) | OK — stays; service from open front |
| AIO 10×54 + WS1 | 10″Ø × ~66″H (+≥12″ above) | Floor near back, east of PT | OK — height 78″ ≪ 106″; service from open front |
| Softener 12×48 + WS1 | 12″Ø × ~60″H (+≥12″ above) | Floor near back, east of AIO | OK — service from open front |
| Brine 18×33 | 18″Ø × ~40″H | Forward of softener toward open front | OK — fill from open front |
| Spin-down + AFV | ~12″L on pipe; 18″ below CL | **LEFT wall** near BACK | OK — AFV drain routes across aisle to back-right receptor |
| Meter + leak SV | In-line ~6″ | LEFT-wall train after spin-down | OK |
| Big Blue 20″ | ~8″Ø × 24″H | LEFT wall, mid-depth | OK — cartridge pull down into aisle |
| 6 gpm limiter | In-line | LEFT wall, pre-UV | OK |
| PRO20 UV | ~4″Ø × ~40″H + ≥36″ pull | LEFT wall; base ~28″ AFF | OK — pull to ~104″ AFF < 106″ |
| UV solenoid | In-line | LEFT wall after UV | OK |
| Main bypass + ISOs | 1″ loop high | ~96″ AFF on LEFT wall | OK — single padlock + reed |
| NEMA 20×16×8 + HA | 20×16 face × 8″ deep | **BACK wall near open right**, ~80″ AFF | OK — door hinged left, swings toward OPEN right; clear of drain air gaps & bypass. Left-wall mount considered; back-near-right is better (keeps train clear, door into open space). |
| 3″ drain + receptor | Standpipe + funnel | BACK-RIGHT at open end of back wall | OK — AFV/AIO/soft/brine each own air gap |
| Kitchen RO | Under sink | Kitchen (not in closet) | N/A |
| 120 V outlets / conduit | — | **Back or left wall only** | OK — no mounts on missing walls |
| Service access | Open front + open right | — | OK — tanks serviceable from open front; no door-swing constraint |

## Flags / best fixes

- Open bay: no door-swing keep-clear; keep ghost 72×40 floor outline for layout discipline.
- Nothing mounts to a non-existent wall (right or front). Automation, outlets, train, bypass → back or left only.
- Back-wall outlets at mid-height may sit behind tanks — prefer ~84″ AFF on the back wall; AFV/UV receptacles on the left wall near the train.
- If pressure tank is larger than 20″Ø, left-train clearance fails — measure existing tank before setting AIO.
- UV lamp pull OK only if PRO20 base ≤~30″ AFF (40″ body + 36″ pull ≤ 106″). Confirm overall length on arrival.
- Gravity drains (brine overflow, AFV flush, any open drain) must fall continuously ≈¼″/ft to air gaps over the BACK-RIGHT receptor — no risers. Prefer downhill for Clack backwash lines too.

## Checks (build)

- Intersection (pipe vs equipment)
- Pipe–pipe clearance ≥ r1+r2+0.5″
- Gravity drains: no uphill segments
- Front orientation: from open front looking at back wall, tank screen-left / drain screen-right
- Enclosure: backplate on an existing wall; door opens into open space
- Mounts: nothing on a non-existent wall
- (Door-swing check removed — no door)

## Drawings
- `closet_plan.png` / `.svg` — top-down (OPEN front + OPEN right)
- `closet_elev_back.png` / `.svg` — back wall tanks + NEMA
- `closet_elev_left.png` / `.svg` — left-wall train + UV pull
- `plumber/wall_layout.png` — schematic elevation (no prices; generic fittings; no push-fit)
