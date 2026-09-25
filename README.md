# elmira-site

Private mirror of https://elmirabakery.wixsite.com/elmira served via nginx on GKE.

## Layout

- `site/` - mirrored pages (index, about, menu, contact)
- `Dockerfile` + `nginx.conf` - nginx on 8080 with pretty routes
- `helm/elmira-site/` - chart, `image.tag` bumps per release
- `.github/workflows/` - `pr-check` (lint+build), `release` (tag+push+deploy)

## Refresh mirror

wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://elmirabakery.wixsite.com/elmira

## Release flow (PR only)

1. Open PR against `main`, wait for `validate` job.
2. Merge PR to `main` triggers release: auto patch tag, image push, chart bump, helm deploy.
3. Each merge maps 1 tag to `helm/elmira-site/values.yaml` image.tag + Chart.yaml appVersion.

## Env

- Project `solid-heaven-334106`, AR `us-central1-docker.pkg.dev/solid-heaven-334106/elmira/elmira-site`
- Cluster `gke-free` (us-central1-a), namespace `elmira`
