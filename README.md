# pavucontrol

Graphical PulseAudio/PipeWire volume control as a charly layer — the
`pavucontrol` GTK mixer for desktop containers.

The `pavucontrol` candy installs the `pavucontrol` GTK mixer and `require:`s
`opencharly/pod-pipewire` — the `pipewire` candy, whose PulseAudio-compatible
server `pavucontrol` connects to. The binary lands at `/usr/bin/pavucontrol` and
is launched on demand (e.g. from the waybar volume indicator), so both its
presence and the audio backend it drives are build-time verifiable.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `pavucontrol` |
| Requires | `pod-pipewire` |
| Binary | `/usr/bin/pavucontrol` |
| Packages | `pavucontrol` (Arch + Fedora arms) |
| Service / port | none (GUI app, launched on demand) |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-desktop-box:
  candy:
    base: fedora-nonfree
    candy:
      - '@github.com/opencharly/layer-pavucontrol:v2026.243.0515'
```

Once deployed, launch the mixer on demand:

```bash
pavucontrol &
```

The waybar `pulseaudio` module has `"on-click": "pavucontrol"` — clicking the
volume indicator in the status bar opens pavucontrol.

## Layout

- `charly.yml` — the `pavucontrol:` candy entity (the `require:` dep, the
  per-distro package arms, and the `plan:` checks) plus the embedded `skill:`
  entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:pavucontrol` — the mixer, its waybar
  integration, and the PipeWire dependency.
- Audio server: `/charly-pod:pipewire`.
- Waybar: `/charly-selkies:waybar`.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
