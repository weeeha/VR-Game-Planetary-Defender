# Planetary Defender — project recovery and vertical slice plan

Date: 2026-09-10  
Status: Proposed project sequence, grounded in a live repository audit. No gameplay implementation performed by this replan.

**Goal:** Recover the earlier prototype and deliver one replayable Montréal defense mission that feels good in VR.

**Architecture:** Preserve recovered systems where they pass fresh checks. Keep tracked-head movement, mech movement, combat, mission state, and presentation separable so that comfort and game rules can be tested independently. Actual code boundaries must be established from recovered source before writing component implementation plans.

**Tech stack:** Historical evidence confirms a Unity project and tests involving OpenXR input. Current Unity version, packages, rendering pipeline, build target, and device support are unknown because project configuration is missing from the inspected repository. Standalone Quest is a planning assumption to confirm at the baseline gate.

**Design source:** [Core gameplay and ability exploration](../../gameplay/core-gameplay-ability-inspirations.md), dated 2026-08-03. The full loadout is explicitly exploratory, not approved.

## What the audit actually found

| Area | Verified evidence | Implication |
| --- | --- | --- |
| GitHub source | `weeeha/VR-Game-Planetary-Defender`, `main`, commit `03b856a49fe356561dbb97a51ad649434f08d75f`, initial commit dated July 30, 2026. The complete tree contains only a 28-byte `README.md`. | There is no gameplay source to review or build from this remote snapshot. |
| Remote work | One branch, no tags, releases, issues, or pull requests returned by the GitHub API. | No alternate published implementation or backlog was found in this repository. |
| Local project mirror | One gameplay exploration document; `sources/` is empty; the mirror is not a Git checkout. | Preserve the design note, but do not treat it as implementation evidence. |
| Historical execution | A local Unity XML report dated August 3, 2026 records 51/51 passing PlayMode tests. | Earlier work existed. These are historical results, not current verification. |
| Historical source location | The report identifies `.worktrees/montreal-vertical-slice/Library/ScriptAssemblies/PlanetaryDefender.PlayModeTests.dll` under the project mirror. That worktree is absent now. | Recovery precedes replacement implementation. Its disappearance does not establish how or why it was removed. |
| Local discovery | No matching project was found through the inspected common workspace folders, Codex worktree folders, filename search, or current Unity Hub project registry. | Source location remains unresolved; this is not proof that every backup or disk lacks it. |
| Current validation | No available source project was compiled, tested, built, installed, or opened in Play Mode during this audit. | Current code quality, visual quality, performance, and physical headset acceptance remain unknown. |

Historical report location: `/Users/nickv/Library/Application Support/Weeeha/Planetary Defender/TestResults.xml`.

The report groups its 51 tests as follows: cockpit calibration (6), health (5), input action contracts (3), mech locomotion (14), runtime player input (14), XR profile compatibility (5), and XR runtime integration (4). Test names describe recentering, tracked-head preservation, wall sliding, slopes, curbs, pause behavior, controller bindings, and comfort effects. This is useful recovery evidence; it does not establish that combat, civilian simulation, or a complete mission was implemented, nor that physical hardware was tested.

## Direction to preserve

- The player pilots a mech defending Montréal.
- Civilian survival determines victory quality.
- The mission is lost only when the player's mech or a critical city target is destroyed: the Hybrid protection rule.
- The catch-and-return shield and sustained primary cannon are the proposed first combat pairing.
- Heavy precision fire, rockets, and Smart Ammo remain candidates. VTOL and traps stay in the idea bank.

Recommended first deliverable: one compact Montréal district, one critical target, one civilian evacuation route, a short sequence of threats, and a clear result/retry loop. A three-to-five-minute mission is a proposed scope target, not an established requirement.

## Options considered

| Approach | Benefit | Cost / risk | Decision |
| --- | --- | --- | --- |
| Recover, verify, then complete a small mission | Preserves prior input/comfort work and exposes the real remaining scope. | Requires locating source or explicitly ending recovery. | Recommended. |
| Start a fresh Unity project immediately | Allows visible development immediately. | Could duplicate or regress previously tested work; would require new stack and control decisions. | Fallback only after the recovery gate. |
| Build the whole loadout and city first | Demonstrates more of the eventual fantasy. | Adds interaction and content complexity before comfort and defense decisions are proven. | Defer. |

## Milestones and exit gates

### 0. Recover and establish a durable source of truth

**Deliverable:** A complete, traceable Unity source checkout in a stable project folder.

- [ ] Locate the former worktree or an exact backup, alternate checkout, Git object store, or user-provided copy. Record provenance before restoring anything.
- [ ] Preserve recovered files and local changes before reconciling with the README-only remote. Do not overwrite another Unity project's files.
- [ ] Verify `Assets/`, `Packages/manifest.json`, and `ProjectSettings/ProjectVersion.txt`. Inspect guidance, scenes, first-party scripts, assemblies, tests, and Git state.
- [ ] Identify the authoritative branch and commit. Record engine/package versions, render pipeline, input stack, target headset, build instructions, and source assets required to reproduce the project.
- [ ] Keep the canonical source outside the replaceable ChatGPT project mirror. Prepare a complete source commit with Unity metadata and an appropriate ignore file; check for private material and asset licensing before publication to this public repository.
- [ ] Produce `docs/AI/UnityProjectContext.md` only once the Unity root is verified.

**Exit:** The project can be opened from its documented location and its source provenance is known. Repository durability is proven by a second checkout once publication is authorized. Publication status must be explicit; a local commit alone is not a remote backup.

**Fallback:** If the bounded recovery search and any user-provided location yield no source, record what was checked and retain the historical evidence. Present a concrete replacement-project proposal before creating a new Unity project. The unavailable prototype must not silently become “nothing was built.”

### 1. Re-establish the playable VR baseline

**Depends on:** Milestone 0, or an explicitly selected replacement baseline.

**Deliverable:** A reproducible headset build with usable cockpit, tracked hands/controllers, calibration, and comfort controls.

- [ ] Open with the recovered project's recorded Unity version; resolve baseline errors before adding features.
- [ ] Discover and rerun available EditMode and PlayMode suites. Compare current results with the historical 51-test report without treating that old count as a guaranteed inventory.
- [ ] Verify the actual startup scene and production player rig; test bindings through real runtime input paths.
- [ ] Check recentering, pause, tracking loss/recovery, turning, and supported seated/standing behavior on the target headset.
- [ ] If locomotion is recovered, verify it rather than removing it. Validate stationary cockpit interaction first, then walking/turning, walls, curbs, and slopes as separate comfort checks.
- [ ] Record source commit, build settings, artifact hash, installation, launch, and the user's physical acceptance separately.

**Exit:** A recorded build runs on the intended headset; controls and calibration work, and physical comfort is acceptable. Editor tests alone do not close this milestone.

### 2. Prove shooting and interception in a small arena

**Depends on:** Milestone 1.

**Deliverable:** A short encounter where firing the primary cannon and catching/returning an incoming attack are both readable and satisfying.

- [ ] Inspect recovered combat first; extend existing behavior where suitable.
- [ ] Implement or finish one sustained primary cannon, one enemy that presents a visible threat, and one clearly catchable hostile projectile type.
- [ ] Give the shield visible ready/capturing/holding/releasing feedback. Start with an aimed release as a provisional accessible interaction; evaluate a throwing gesture only after basic reliability is demonstrated.
- [ ] Establish ownership and damage rules for returned projectiles so they cannot repeatedly damage the same target or immediately strike the player after release.
- [ ] Validate weapon/shield simultaneity, aiming, arm fatigue, and visibility from the cockpit on hardware.

**Exit:** The player can identify an incoming attack, intercept it intentionally, and return it to a target reliably. Measure failed attempts and investigate their causes before adding weapons. Add focused automated tests for damage, projectile ownership, capture/release, and reset behavior; use play sessions for feel.

### 3. Make civilian protection change the mission

**Depends on:** Milestone 2.

**Deliverable:** One complete mission with distinct victory grades, loss states, and clean retry.

- [ ] Build a graybox district with one critical target and a simple evacuation route. Use simple groups or a visible evacuation representation before investing in crowd simulation.
- [ ] Route readable enemy threats toward the mech, critical target, or civilians so the player must choose what to protect.
- [ ] Implement the Hybrid protection rule exactly: civilian casualties reduce victory quality; mech or critical-target destruction ends the mission in defeat.
- [ ] Introduce a finite encounter sequence and an explicit completion condition. Show the damage/civilian consequence and final result clearly.
- [ ] Ensure retry restores mission health, civilians, enemies, projectiles, score, and player state without stale callbacks or duplicate spawns.

**Exit:** Validate high-survival victory, lower-survival victory, mech defeat, critical-target defeat, and repeated retry. A player should be able to explain why protection changed their result. Make rule and reset tests automated; validate threat readability on the headset.

### 4. Produce the Montréal vertical slice

**Depends on:** Milestone 3.

**Deliverable:** One polished, replayable district with recognisable Montréal identity and stable performance on the target hardware.

- [ ] Prove the visual direction on a small representative street/city view before extending it across the district.
- [ ] Add scale cues, cockpit feedback, directional audio, enemy attack warnings, readable civilian status, and a short contextual introduction.
- [ ] Select and record the target headset refresh mode and corresponding frame-time budget. Profile the busiest encounter on device; use measured bottlenecks to guide pooling, VFX, geometry, and lighting work.
- [ ] Run complete missions and repeated retries long enough to observe sustained performance and comfort. Record build/commit, hardware, duration, measurements, and physical feedback.
- [ ] Address observed problems, then produce a short capture from the verified build and an evidence summary.

**Exit:** A new player can start, understand the protection objective, complete or lose the mission, interpret the result, and retry. Sustained device performance and physical acceptance meet the recorded target. A video capture alone cannot close those checks.

### 5. Expand only in response to play evidence

**Depends on:** Acceptance of Milestone 4.

Choose one addition per iteration:

| Candidate | Add when the observed problem supports it |
| --- | --- |
| Heavy precision shot | The primary cannon provides too little distinction between deliberate weak-point attacks and sustained fire. |
| Rockets | A separate burst-damage choice improves defense decisions enough to justify its control and cooldown. |
| Smart Ammo | A temporary earned state helps manage multi-target surges without erasing the need to prioritize protection. |
| More enemies or districts | The basic interaction remains engaging and additional encounters can be built without changing core systems. |
| VTOL / traps | Specific positioning or area-defense needs remain unresolved after simpler encounter changes. |

Smart Ammo requires a separate design decision about meter rewards, valid targets, targeting near civilians, and its relationship to rockets. Neither the exploration note nor this plan establishes those rules as approved.

## Immediate next work

The next implementation task is **source recovery and baseline verification**, not a weapon expansion. Once the Unity source is available, replace uncertainty with a concrete inventory and write a component-level implementation plan against actual file paths. Do not invent source filenames or promise completion dates before that inventory.

Use milestone gates as the schedule until availability, recovery scope, and hardware access are known. End each work session with: verified outcome, evidence location, unresolved physical/external checks, and the next milestone blocker.

## Changes made by this replan

- Changed sequencing to recovery → VR baseline → two-tool combat → protection mission → Montréal presentation/performance → expansion.
- Preserved the Hybrid protection rule and the existing ability exploration.
- Distinguished an empty remote from evidence of an earlier tested local prototype.
- Separated historical tests, fresh tests, build, install, launch, visuals, performance, and physical acceptance.
- Deferred full city production and the full ability set until the core mission earns them.

This document is a project roadmap. It does not claim that a missing source project has been recovered, that the old tests pass today, or that the proposed scope has already been implemented.
