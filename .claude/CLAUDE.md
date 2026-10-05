# myungchulkim.com

Static, hand-written HTML served by GitHub Pages from `main` (custom domain in `CNAME`).
Pushing to `main` deploys in about a minute. The owner also edits through the GitHub web
UI, so fetch and compare with `origin/main` before committing. This file lives in
`.claude/` because Jekyll skips dot-folders; a root `CLAUDE.md` would be published.

## Keep the repository small

Git keeps every committed version of a binary forever, so manage size before a file is
committed, not after. The pack was about 111 MiB in October 2026.

- Check before committing: `du -h <files>` for anything new, and `git count-objects -vH`
  afterwards. Nothing new over a few MB goes in without being compressed first.
- Images: at most 1600 px wide. JPEG (quality about 82) for photos and 3-D renders, PNG
  for plots and line art; aim for under 400 KB each. Never commit the raw 3000 px renders
  from the paper repos.
- PDFs: compress anything over about 5 MB with
  `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -dDetectDuplicateImages=true -o out.pdf in.pdf`,
  then render a page and check it is still legible. Aim for under about 10 MB per file.
- Video and animations: H.264 MP4, at most 720 px, `+faststart`, no audio. GIFs under
  about 1.5 MB (the recipe is in the header comment of `research/accel_atomistic.html`).
- Get a large file right the first time. Committing a big file and then a smaller
  replacement keeps both in history. Fix it by amending before pushing; rewriting pushed
  history needs a backup (`git bundle create backup.bundle --all`) and
  `git push --force-with-lease`.
- When a page stops referencing a file, delete the file in the same change.
- GitHub warns at 50 MB per file and rejects 100 MB; stay far below both.
