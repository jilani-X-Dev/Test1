# Testing and Verification

BadgeQuest is a static browser app. It has no build step, backend, API token, or package installation. Verification therefore combines a browser smoke test with Markdown/link checks.

## Run the app

1. Open `index.html` directly in a modern browser, or serve the repository root with a local static server.
2. Open the browser developer tools and check the Console for errors.
3. Confirm the page title, introduction, active achievement cards, historical cards, and footer links render.

## Browser smoke-test checklist

- [ ] The initial summary shows 3 earned achievements, 4 active goals, and 43% planner progress.
- [ ] The **All**, **Earned**, **Goals**, and **Historical** filters show only the matching cards.
- [ ] Each non-historical card can be toggled between earned and goal states.
- [ ] The summary counts and percentage update after a card is toggled.
- [ ] Reload the page and confirm manual changes persist in the same browser.
- [ ] Use **Reset manual changes**, accept the confirmation, and confirm the original checklist state returns.
- [ ] Historical cards are visible in the historical section and cannot be toggled.
- [ ] Achievement detail links open the expected GitHub or documentation page in a new tab.
- [ ] The layout remains usable at narrow mobile widths and at desktop widths.
- [ ] Keyboard users can reach filters, checklist buttons, reset, and links; focus remains visible.
- [ ] With reduced-motion enabled in the operating system, transitions are reduced.
- [ ] The browser console contains no uncaught JavaScript errors during the checks.

## Markdown and repository checks

- [ ] Confirm the README describes the current repository accurately.
- [ ] Open each relative Markdown link and confirm its target exists.
- [ ] Check headings, lists, code formatting, spelling, and date references.
- [ ] Review the diff for accidental or unrelated changes.
- [ ] Confirm no secrets, local environment files, or generated files were committed.
- [ ] After a pull request is merged, verify the changed files on `main`.

## Local Markdown link check (PowerShell)

Run this from the repository root to find common relative Markdown links whose targets do not exist:

```powershell
$files = Get-ChildItem -Recurse -File -Filter *.md
foreach ($file in $files) {
  $content = Get-Content $file.FullName -Raw
  foreach ($match in [regex]::Matches($content, '\\[[^\\]]+\\]\\(([^)#]+)(?:#[^)]+)?\\)')) {
    $target = $match.Groups[1].Value.Trim()
    if ($target -match '^https?://' -or $target.StartsWith('#')) { continue }
    $resolved = Join-Path $file.DirectoryName $target
    if (-not (Test-Path $resolved)) {
      Write-Host "Missing link: $($file.Name) -> $target"
    }
  }
}
```

This is a lightweight link check, not a complete Markdown parser. It does not validate external URLs, reference-style links, or every Markdown syntax variant.
