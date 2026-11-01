# Shiori LazyCat community package

Upstream https://github.com/go-shiori/shiori (MIT), v1.8.0. Package `community.lazycat.app.shiori`, min OS 1.5.0, amd64, mirror delivery, community (喵喵) store only. Official candidate `io.zeroc.app.shiori` (id 597) is a separate implementation; this package is an independent community build.

Shiori is a single-container Go bookmark manager. It defaults to SQLite stored under `SHIORI_DIR`, so no external database is needed. One bind keeps bookmarks, tags, archive snapshots and the database together:

    /lzcapp/var/data:/shiori

Image delivery is verified: `ghcr.io/go-shiori/shiori:v1.8.0` and `ghcr.1ms.run/go-shiori/shiori:v1.8.0` resolve to the same linux/amd64 digest.

`SHIORI_HTTP_SECRET_KEY` is derived from a platform `stable_secret`; upstream otherwise generates a random UUID per start and invalidates every session on restart.

The login page is the Vue single-page route `/login`, so autofill runs in the browser phase and is restricted to `form input[type="text"]` and `form input[type="<password>"]` on that path only. It never submits automatically and never touches other forms; the account must still be created on first use with the same credential shown in the deployment parameters. The app stays behind the LazyCat entry login.

Not device-tested: account creation, login, bookmark CRUD, archive snapshots, import/export, and persistence across restarts. No smoke test, extra healthcheck, startup gate or file-picker interception was added.
