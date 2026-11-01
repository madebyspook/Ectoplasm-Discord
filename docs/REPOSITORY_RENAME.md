# Repository rename checklist

The repository and local checkout are named `Ectoplasma-Discord`. The theme name remains `Ectoplasma`; distribution filenames, variables, and styling are unchanged. `package.json` supplies the new repository and Pages URLs to the build; never edit the generated CSS manually.

## Before merging

- Keep the rename changes on a feature branch targeting `main`. Do not merge as part of the rename task.
- Keep the existing Pages publishing source. Renaming the repository does not deploy the feature branch to production.
- GitHub repository links redirect, but old GitHub Pages paths do not. Previously installed loaders need the migration below. A deployment gap is possible between the repository rename and merging/deploying these changes.
- Other clones should run `git remote set-url origin https://github.com/madebyspook/Ectoplasma-Discord.git`. Close watchers before renaming local folders, then reopen the renamed checkout in the editor and restart them.

## After merging

1. Confirm the existing GitHub Pages deployment for `main` succeeds. If necessary, trigger a rebuild using the existing Pages setup; do not change its publishing source to the feature branch.
2. Fetch `https://madebyspook.github.io/Ectoplasma-Discord/Ectoplasma.theme.css` and `https://madebyspook.github.io/Ectoplasma-Discord/dist/Ectoplasma.css`. Both must return HTTP 200 and CSS content, rather than an HTML error page.
3. Check that the downloaded loader has `@name Ectoplasma`, the new repository `@source`, and `@updateUrl https://madebyspook.github.io/Ectoplasma-Discord/Ectoplasma.theme.css`. Its single import must be `https://madebyspook.github.io/Ectoplasma-Discord/dist/Ectoplasma.css` and precede user configuration. Verify the live files match the merged generated outputs.
4. Back up installed loader customizations. Download and replace `Ectoplasma.theme.css`, then restore the configuration below the import. For an existing customized loader, changing only the repository path in its import and metadata URLs also preserves settings. Automatic loader updates are not guaranteed.
5. In BetterDiscord, enable only Ectoplasma and reload Discord. Confirm the new import succeeds in the network panel and compare the affected views with the previous appearance, including accent, background modes, and BackgroundManager integration when used. Record actual Discord/BetterDiscord versions and results. Automated build and URL checks do not establish runtime compatibility.
6. Update any external bookmarks, profile links, or integrations that contain the former repository or Pages URLs. Historical release assets and installed files are not rewritten by this PR.

A compatibility site at the old Pages path would require a separate hosting decision. Recreating the old repository name also removes GitHub's repository redirect; do not do that merely to restore old Pages links.
