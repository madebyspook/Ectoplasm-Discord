# Ectoplasm

A dark BetterDiscord theme featuring translucent glass surfaces, electric blue accents, and neon glow effects.

## Installation

1. Install [BetterDiscord](https://betterdiscord.app/).
2. [Download Ectoplasm.theme.css](https://madebyspook.github.io/Ectoplasm-Discord/Ectoplasm.theme.css).
3. Open **Discord → Settings → BetterDiscord → Themes → Open Themes Folder** and place the downloaded file there.
4. Enable **Ectoplasm**.

## Configuration

Open `Ectoplasm.theme.css` in a text editor or BetterDiscord's theme editor to customize its appearance.

- **Accent color:** Change `--spook-accent` to your preferred color.
- **Background:** Choose between a solid color, custom wallpaper, or BackgroundManager wallpaper by uncommenting the corresponding configuration.
- **macOS Vibrancy:** Disable `--spook-background-image`, then enable **Transparency** in BetterDiscord's Window Preferences and select a macOS Vibrancy effect. Restart Discord to apply the window settings. This allows the desktop to show through transparent areas of the theme. (note blur in collapsed panels from Collapseable UI doesn't work)
- **Additional customization:** Adjust other theme variables using BetterDiscord's Custom CSS.

Keep the `@import` line intact. Your configuration changes may be overwritten when replacing the theme file.

## Plugin Support

- **[CollapsibleUI](https://betterdiscord.app/plugin/CollapsibleUI)** — Collapsed panels appear as blurred, translucent overlays.
- **[BackgroundManager](https://betterdiscord.app/plugin/BackgroundManager)** — Use wallpapers managed by BackgroundManager as the theme background.