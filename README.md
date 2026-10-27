# media-archive

The public **Archive** on the Endless Library forum: photos and video from library events,
browsable by anyone and posted by members.

- Forum: https://shush.endlesslibrary.com.au/c/archive
- Media files: Cloudflare R2 bucket `endless-uploads`, served from `media.endlesslibrary.com.au`

This repo holds no code that Discourse installs. It's the documentation and config for how the
archive is set up, so whoever looks after it next can see what was done and why.

## What's here

| Path | What it is |
|---|---|
| [`RUNBOOK.md`](RUNBOOK.md) | Step-by-step setup, in order. Start here. |
| [`config/app.yml.snippet`](config/app.yml.snippet) | The lines added to `/var/discourse/containers/app.yml`. Placeholders only, no secrets. |
| [`config/r2-cors.json`](config/r2-cors.json) | CORS policy pasted into the R2 bucket settings. |
| [`content/archive-about.md`](content/archive-about.md) | Text for the Archive category's About topic (posting guidelines + photo policy). |

## How it works

1. A member creates a topic in the Archive category and drags in photos or an MP4.
2. Discourse uploads the file straight to the R2 bucket, not to the VPS disk.
3. The post shows images (tiled with `[grid]`) and an inline video player.
4. The Topic List Thumbnails component shows the category as a masonry gallery.
5. Each week, rclone copies the bucket to a second provider as a backup.

## Setup status

- [ ] 0. Prerequisites checked (DNS on Cloudflare, backup taken)
- [ ] A. R2 bucket, custom domain, API token, CORS
- [ ] B. Discourse pointed at R2, rebuilt, verified
- [ ] C. Upload limits and file types
- [ ] D. Archive category, tags, permissions
- [ ] E. Gallery view (Topic List Thumbnails)
- [ ] F. About topic posted
- [ ] G. Weekly bucket backup scheduled

## Secrets

Never commit the R2 access keys or any other credential here. They live in `app.yml` on the
server and in the library's password manager.
