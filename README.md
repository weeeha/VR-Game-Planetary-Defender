# VR Game — Planetary Defender

**Problem.** A mech game about defending a city needs a reason for the player to care about the people in it.

**Idea.** The player pilots a mech defending Montréal, and civilian survival determines victory quality. A mission is lost only when the mech or a critical city target is destroyed.

**Built.** Docs and plans only so far: a recovery and vertical-slice plan and gameplay notes. A local Unity report from August 3 records 51 passing PlayMode tests, but the source has not been located, so gameplay, build and headset readiness are unverified. 2 commits on 2 days, Jul 30 to Sep 28, 2026.

**Decision.** Recover and verify the earlier Unity project before building anew. Starting a fresh project immediately could duplicate or regress the input and comfort work the tests already covered, so it stays a fallback after the recovery gate.

A VR mech game about defending Montréal, with civilian survival determining victory quality.

## Current status

The September 10, 2026 audit found that the published repository contained only its initial README. A historical local Unity report records 51 passing PlayMode tests on August 3, but the corresponding source worktree has not been located. Current gameplay, build, and headset readiness are therefore unverified.

## Project documents

- [Recovery and vertical slice plan](docs/superpowers/plans/2026-09-10-project-replan.md)
- [Core gameplay and ability exploration](docs/gameplay/core-gameplay-ability-inspirations.md) — preserved August 3 notes; the full loadout remains exploratory.

The next milestone is to recover and verify the earlier Unity project, then complete one small, playable Montréal defense mission.
