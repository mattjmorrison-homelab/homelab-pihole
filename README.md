# homelab-pihole

Pi-hole deployment, including local DNS overrides for `*.morrisons.site`
ingress hostnames and a handful of `.local` LAN devices
(`manifests/templates/configmap-local-dns.yaml`).

## Static IP reservations

Every device with a `.local` entry in `configmap-local-dns.yaml` needs a
static/reserved IP on the LAN, or its DNS entry goes stale the next time
DHCP hands it a different address:

| Hostname | IP |
|---|---|
| `imac` (all `*.morrisons.site` entries) | 192.168.68.84 |
| `Matthews-MacBook-Air.local` | 192.168.68.71 |
| `nevespc.local` | 192.168.68.100 |
| `pi1.local` | 192.168.68.92 |
| `pizero.local` | 192.168.68.93 |
| `basementpc.local` | 192.168.68.78 |

These are currently reserved in the Deco app (for right now — the router
setup itself may change later): **More** (the four-square icon) →
**Advanced** → **Address Reservation**.

If a device's actual IP ever stops matching its reservation, update both
the reservation in Deco and the corresponding `address=` line in
`configmap-local-dns.yaml` — they have to stay in sync.
