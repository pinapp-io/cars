# @pinapp-io/cars

A pinapp for vehicle logbooks. Each minted instance represents one car —
identified by year/make/model/VIN — and accumulates fueling, service, photo,
and note events. The QR code printed at mint goes inside the glove box.

Built on [`@pinapp-io/harness`](https://github.com/pinapp-io/harness).

## Install on epistery-host

### Local dev (symlink)

```bash
ln -s /path/to/pinapp/cars ~/.epistery/.agents/cars
# restart epistery-host
```

After restart, `http://localhost:4080/admin#services` will list **Cars**.
The agent mounts at:

- `/agent/pinapp-io/cars` — landing / mint a new car
- `/agent/pinapp-io/cars/admin` — access control (ACL widget)
- `/agent/pinapp-io/cars/{address}` — a specific car's logbook (QR target)

### Production (registry)

Ask the epistery.host operator to add `https://github.com/pinapp-io/cars`
to the registry at `https://epistery.host/agent/epistery/registry/admin`.
Once registered, any epistery-host instance can install Cars from its
services UI. See the [harness README](https://github.com/pinapp-io/harness#making-a-pinapp-available)
for the full registration story.

## What the harness gives you for free

Everything except the template:

- The on-chain factory contract (shared across all pinapps on a domain)
- Instance JSON storage at `~/.epistery/{domain}/cars/instances/`
- Image storage via the domain's configured backend
- ACL enforcement (Reader/Editor/Admin) keyed on `pinapp-io/cars`
- Refinery enrichment — every event gets geo + weather context
- The `/admin` ACL widget

This package contributes only:

- `template/template.json` — fixed attributes (year/make/model/VIN/color/plate)
  and event types (Fuel/Service/Photo/Note)
- `template/mint.html` — the create form
- `template/app.html` — the mobile-first instance UI
- `template/icon.svg` — the icon
- `index.mjs` — three lines of glue calling `createPinappAgent({...})`
