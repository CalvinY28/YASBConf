# QuickShell glass for YASB

A Windows adaptation of [my QuickShell configuration](https://github.com/CalvinY28/MyArch/tree/main/.config/quickshell), built against **YASB 2.0.7**.

The default layout is a compact, centered glass island with a settings button, 24-hour clock, notification button, and workspace dots outside either edge. It uses the QuickShell bar's 36px height, 10px top offset, subtle white fill, and bright active dots. Workspace 1 sits nearest the clock on both sides.

## Install / try this branch

If this repository is already your active YASB config directory, run these commands there:

```powershell
git fetch origin
git switch --track origin/quickshell-glass
```

If the local branch already exists, use `git switch quickshell-glass`. Commit or stash any local edits first if Git reports a conflict. YASB watches both files and reloads them on save; restart YASB from its tray menu if the layout does not refresh.

If your checkout lives elsewhere, copy **both** `config.yaml` and `styles.css` into `$env:USERPROFILE\.config\yasb` (or your `YASB_CONFIG_HOME` directory). Back up your current two files first.

To return to the original configuration, switch back to `main`, or restore your saved files.

## Controls

| Control | Action |
| --- | --- |
| Settings button, or Win+Alt+C | Open the glass control center |
| Clock: left-click | Open calendar |
| Clock: right-click | Toggle seconds within the same clock width |
| Notification button: left-click | Open Windows notification center |
| Notification button: right-click | Show notification count instead of the icon |
| Workspace dot: click | Switch Komorebi workspace |
| Workspace dots: scroll | Cycle Komorebi workspaces |

The control center contains media playback and artwork, brightness and volume sliders with device selection, power plans/modes, session lock and power controls, and shortcuts for Wi-Fi, Bluetooth, Night light, screenshot capture, Command Prompt, and Task Manager. Wi-Fi, Bluetooth and Night light buttons **open their Windows settings pages**. They do not display connection state or toggle those features directly.

Workspace dots represent your actual Komorebi workspaces, in mirrored order. They hide when Komorebi is offline. This configuration does not create workspaces or install a window manager. Configure your preferred number in Komorebi.

## Optional side islands

Your existing launcher, taskbar, memory, traffic, battery and tray widgets are still defined. To show them, replace the empty `left` and `right` lists under `bars.status-bar.widgets`:

```yaml
left: [launch_tools]
# Keep the existing center list.
right: [system_tools]
```

The launcher’s Alt+Space shortcut is available when `launch_tools` is enabled. Volume, wallpaper and power-menu widgets also remain available to add to either group. Wallpaper post-change hooks were removed because `yasb.ps1` is not in this repository and the `wal` dependency was not provided.

## What differs from QuickShell

- The control center and calendar are separate popups. This theme does not implement the QML bar's expanding rectangle, close-on-pointer-leave behavior, three-page carousel, refraction shader, or spring/metaball animations.
- The terminal and system shortcuts launch Windows applications. There is no embedded terminal or inline system-monitor panel in the default compact layout.
- YASB's native adaptive shape supplies the glass surface; its corner shape differs slightly from QuickShell's rounded rectangle.
- Brightness and media availability depend on the display hardware and Windows media session support. Native notification center keeps Windows styling.
- The bar reserves 46px at the top and hides for fullscreen applications.

The clock prefers JetBrainsMono NFP and falls back to Cascadia Mono or Consolas. Control-center icons use Segoe Fluent Icons. Optional legacy widgets use Nerd Font glyphs, as in the original configuration.

## Validation

Checked the root/bar configuration and all 17 widget definitions with the upstream YASB v2.0.7 Pydantic models. Processed the stylesheet with YASB's CSS processor and checked the centered clock, mirrored Qt workspace layout, and single glass island in an offscreen Qt layout harness.

The full Windows application, DWM blur, Komorebi switching, hardware controls and Windows commands could not be exercised in the Linux editing environment. After loading, check that the clock/calendar, control center, notifications and workspace clicks work; share a screenshot for visual tuning.

References: [YASB configuration](https://github.com/amnweb/yasb/blob/v2.0.7/docs/Configuration.md), [styling](https://github.com/amnweb/yasb/blob/v2.0.7/docs/Styling.md), and [control-center options](https://github.com/amnweb/yasb/blob/v2.0.7/docs/widgets/%28Widget%29-Control-Center.md).
