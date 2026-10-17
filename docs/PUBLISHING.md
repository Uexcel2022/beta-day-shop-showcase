# Publishing and maintaining the showcase

**Public presentation repository:** [Uexcel2022/beta-day-shop-showcase](https://github.com/Uexcel2022/beta-day-shop-showcase)

This checkout is independent of the private application repository. Only approved documentation, selected code pictures and gallery assets belong here. The complete [application source](https://github.com/Uexcel2022/beta-day-shop) remains private.

## Publishing an update

1. Review the changed documents and pictures. Use synthetic presentation records, keep runtime credentials out of screenshots, and retain relevant image attribution.
2. Update the source snapshot and evidence dates when the application changes. Update the SHA-256 entries in SHOWCASE-MANIFEST.json for any changed package files.
3. From this showcase checkout, inspect and commit only the intended presentation changes:

```powershell
git status --short
git add README.md CREDITS.md SHOWCASE-MANIFEST.json docs assets .gitignore .gitattributes
git diff --cached --check
git commit -m "Update application showcase"
git push origin main
```

4. Open the repository while signed out and confirm the README, images and document links render.
5. Keep the confirmed public showcase link on the CV; [CV wording](CV-ENTRY.md) is provided.

Public repository hosting displays these documents and pictures. The commerce application itself is demonstrated locally; it has not been deployed as a public website. Payments and refunds remain simulated.

The source repository's visibility is independent of this public showcase. No full application source or runnable credentials are distributed here. No open-source license grant is included; photograph attribution remains in [CREDITS](../CREDITS.md).
