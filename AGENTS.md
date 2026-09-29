# AGENTS.md — layer-pavucontrol

Standalone candy repo for the `pavucontrol` layer — the PulseAudio/PipeWire GTK
volume-control mixer for desktop containers. The candy lives in `charly.yml` at
the repo root: the `require:` on `pod-pipewire`, the per-distro package arms, the
`plan:` checks, and the embedded `skill:` entity projected into the marketplace
corpus as `/charly-selkies:pavucontrol`.

Canonical files:

- `charly.yml` — the `pavucontrol:` candy entity and the `pavucontrol-skill:`
  skill entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:pavucontrol` — the owning skill. The mixer, its waybar
  integration, and the PipeWire dependency. Load before editing or
  troubleshooting.
- `/charly-pod:pipewire` — the audio server this candy requires but does not own.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, and service
  declarations). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps assert the binary, the package record, and
  the PipeWire server binary are present.

## Modify this repo

- Edit the `pavucontrol:` candy entity AND the `pavucontrol-skill:` skill entity
  in `charly.yml` together. The skill is the projected usage source.
- Keep both distro arms (`arch`, `fedora`) in step — the candy is
  cross-distro, and a package-name change on one arm must be mirrored.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo — read it
  before landing.
- Release history lives in `CHANGELOG/`.
