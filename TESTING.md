# Testing and Verification

This repository currently contains documentation only, so validation focuses on Markdown structure, links, and GitHub workflow.

## Manual checklist

- [ ] Confirm the README describes the repository accurately.
- [ ] Open every relative Markdown link and confirm its target exists.
- [ ] Check headings, lists, code formatting, and spelling.
- [ ] Review the diff for accidental or unrelated changes.
- [ ] Confirm no secrets, local environment files, or generated junk were committed.
- [ ] Open the pull request and verify that its title, summary, and issue links are correct.
- [ ] After merge, verify the files on `main`.

## Local link check

From the repository root, run this PowerShell snippet to identify local Markdown links whose target does not exist:

```powershell
$files = Get-ChildItem -Recurse -Filter *.md
foreach ($file in $files) {
  $content = Get-Content $file.FullName -Raw
  foreach ($match in [regex]::Matches($content, '\\[[^\\]]+\\]\\(([^)#]+)(?:#[^)]+)?\\)')) {
    $target = $match.Groups[1].Value
    if ($target -match '^https?://' -or $target.StartsWith('#')) { continue }
    $resolved = Join-Path $file.DirectoryName $target
    if (-not (Test-Path $resolved)) {
      Write-Host "Missing link: $($file.Name) -> $target"
    }
  }
}
```

The snippet is a lightweight local-link check, not a full Markdown linter. It does not validate external URLs or every Markdown link syntax.
