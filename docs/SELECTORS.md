# Maintaining Discord selectors

`src/abstracts/_classes.scss` owns Discord class names and semantic typography selectors. It emits no CSS. Section files import it as `classes` and keep the existing scope, states, declarations, and cascade order:

```scss
@use "../abstracts/classes";

#app-mount #{classes.$channel-wrapper-unread} #{classes.$channel-name} {
    filter: var(--spook-glow-filter-strong);
}
```

Keep stable selectors such as `#app-mount`, picker panel IDs, roles, and `data-layer` attributes when they reliably identify the existing target. Typography aliases use observed `data-text-variant` attributes instead of generated utility classes. They retain class-level specificity and remain scoped by their surrounding section selectors. Avoid generic replacements such as `[class*="container_"]`.

## Updating mappings

1. Inspect the affected element and its ancestors in live Discord. Check default, hovered, selected, and unread states separately. Open dialogs, popouts, and lazy-loaded views before inspecting them.
2. Find the semantic alias in `_classes.scss`. Treat another theme's mappings as candidates: a matching suffix does not establish that two components are the same. Discord can rename a hook or split a module as well as regenerate its hash.
3. Verify the candidate against the intended live element and computed styles. A class present in Discord's loaded CSS is useful supporting evidence, but does not verify an unopened view. Change section structure only when the live DOM requires it.
4. Update the alias, preserving surrounding selectors and declaration order. Keep all new Discord class hashes in `_classes.scss`; do not scatter them through sections or modify generated CSS manually.
5. Run `npm run build`, `npm run check`, `npm test`, and `git diff --check`. For selector-only migrations, compare ordered declarations with a fresh pre-change Sass compilation. These checks do not replace Discord testing.
6. Use the existing development workflow to test in BetterDiscord. Keep development writes in place, enable only the intended theme, and confirm that the loaded stylesheet is the new build. Preserve user configuration and report unopened views as unverified.

The November 2026 migration used [Translucence's selector update](https://github.com/CapnKitten/BetterDiscord/commit/f71e4ff4af69e13b7a36b283a56c9d040b45fb07) as a mapping reference, checked against Discord 0.0.421. Ectoplasm's design, tokens, mixins, and declarations were retained. Live inspection also resolved mappings missing or stale in that reference, including settings typography, the channel-settings guard, forum card details, and voice text chat.

BackgroundManager is optional in solid mode. A missing `--bgm-url` does not explain a selector failure when the active background image and tint are both `none`. Keep plugin troubleshooting separate from selector maintenance.

## Validation on November 7, 2026

The migration centralizes 296 class identities and seven typography selectors. All 296 class identities were found in Discord's loaded native CSS or live DOM after opening the relevant views. Chromium accepted all 226 compiled selector blocks. This establishes selector availability, not visual coverage of every state.

`npm run build`, `npm run check`, and all seven `npm test` tests passed. A fresh pre-change Sass compilation and the migrated compilation contained the same 226 ordered declaration blocks: values, property order, and `!important` flags were unchanged. The final selectors matched the explicit old-to-new migration. No selector aliases were unresolved or unused, and no referenced `--spook-*` token was undefined.

| Surface | Live validation |
| --- | --- |
| Application, channel/server lists, chat, composer | Restored tinted backgrounds, text colors, glass/glow, and transparent inner layers |
| Unread/selected channels and server indicators | Computed accent colors, shadows, and filters |
| Channel hover | Computed neon text, selection tint, and glow under a temporary DevTools hover state; state cleared afterward |
| Code blocks | Glass background, border, primary text, and blue box glow retained |
| Members list | Background, blur, and group-heading colors |
| Direct messages and Friends | List backgrounds, author colors/no shadow in DMs, friend/status colors, selected tab, and Friends wallpaper |
| Add to DM dialog | Scoped glass, blur, and glow; no group was created |
| Forums | Card background/blur/glow, titles, previews, tags, counts, and wallpaper |
| Channel settings | Live guard, wallpaper, sidebar blur, content tint, form glass, and category color; no settings saved |
| User settings | Modal/sidebar/header surfaces, typography, and the current default-keybind groups |
| Search | Suggestion glass/blur, semantic text variants, dark results panel, and transparent result cards |
| Threads and context menus | Threads browser/header glass; transient menu glass, blur, glow, and label colors captured before focus changed |
| Emoji, GIF, sticker pickers | Glass/blur and search layers; transparent headers/categories and GIF category labels |
| Browse Channels | Wallpaper, row tint, primary names, and secondary descriptions |
| Voice preview and floating text chat | Wallpaper, outer blur, and transparent inner surfaces; no call joined |
| Background modes | Active solid mode verified; temporary gradient-backed wallpaper composition verified and original inline/configuration state restored |

Transient tooltips, forum-channel hover previews, connected-call/speaking states, and other unopened content-specific states remain visually unverified. Their class mappings exist in native CSS. External wallpaper image loading and BackgroundManager operation were not tested; the plugin remains independently broken.

The active EctoplasmDev stylesheet matched the installed development file, and its styling matched the regenerated distribution stylesheet. The existing watcher performed development writes; no production deployment was made. User configuration was preserved byte-for-byte. Task-file whitespace checks passed; the full working-tree check still reports the three pre-existing trailing-space lines in `_configuration.scss`, which were intentionally left untouched.
