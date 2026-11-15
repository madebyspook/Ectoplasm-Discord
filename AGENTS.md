# Ectoplasm — Agent Instructions

Ectoplasm is a BetterDiscord theme with dark translucent surfaces, customizable accents, and neon glow effects. Preserve its existing appearance and functionality unless explicitly requested otherwise.

## Source and Distribution

- `src/main.scss` is the authoritative, ordered SCSS entry point. Preserve its module order.
- `src/abstracts/` contains CSS custom properties, configuration, and shared Sass mixins.
- `src/sections/` groups styles by Discord interface area.
- `package.json` supplies production metadata. Keep its version synchronized with `package-lock.json`.
- `scripts/build.mjs` generates the root `Ectoplasm.theme.css` loader and the hosted `dist/Ectoplasm.css` stylesheet. Never edit generated CSS manually.
- Preserve the remote-loader architecture, public filenames, and GitHub Pages URLs unless explicitly requested otherwise.
- A release tag does not freeze the remotely hosted stylesheet.

## Styling

- Scope selectors to the intended Discord interface area. Avoid unintended changes to specificity, declaration order, `!important`, and cascade behavior.
- Preserve existing `--spook-*` variable names and their distinct purposes. Similar values do not make variables interchangeable.
- Reuse existing Sass mixins where appropriate. Avoid abstractions that add complexity without meaningful benefit.
- Preserve BackgroundManager integration, wallpaper configuration, and macOS Vibrancy behavior unless explicitly requested otherwise.
- Do not change suspected outdated Discord selectors speculatively. Verify them against the live client when possible, or identify what requires manual inspection.

## Build and Development

- Use the existing local Dart Sass dependency.
- `npm run build` generates the production loader and stylesheet without installing them into BetterDiscord.
- `npm run build -- --watch --dev` watches source changes and updates the installed `EctoplasmDev.theme.css`.
- Write the installed development theme in place, never through atomic replacement. BetterDiscord may unload atomically replaced theme files.
- Repository-generated outputs may use atomic replacement.
- `npm run check` is read-only and verifies generated outputs and metadata consistency.
- Use temporary fixtures for tooling tests, never the user's actual BetterDiscord themes directory.
- When preserving appearance is essential, compare compiled CSS against a baseline, excluding only metadata and comment differences.

## Documentation and Distribution

- Keep end-user installation instructions separate from contributor setup.
- Keep `README.md`, `CONTRIBUTING.md`, and GitHub templates consistent with the actual project behavior.
- Do not invent screenshots, compatibility results, release notes, or release history.
- Do not choose or add a license without an explicit owner decision.
- Do not change GitHub Pages configuration, repository settings, or hosting infrastructure without explicit permission.
- Do not claim Discord runtime compatibility or visual verification without testing the live client.

## Handoff

- Report any remaining Discord-specific visual checks or manual steps.
- Distinguish automated build results from actual Discord runtime testing.
- Ask before making decisions that significantly affect the theme's appearance, architecture, or distribution.