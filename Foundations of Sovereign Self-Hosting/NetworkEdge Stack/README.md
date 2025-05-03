# Sovereign Edge Network Stack

This is a minimal, self-hosted edge networking stack that enables secure remote access to internal services using Cloudflare Tunnel and Traefik, paired with local DNS control using Pi-hole and Unbound.

## 📁 Contents

- `docker-compose-netedge.yml` — Compose file defining the core network services  
- `traefik.netedge.yml` — Static configuration for Traefik (reverse proxy)  
- `cloudflare.config.netedge.yml` — Cloudflared tunnel config file  
- `cloudflare.yourtunnelid.json` — JSON credentials for Cloudflared tunnel  
- `unbound.netedge.conf` — DNS resolver config for Unbound  

---

## 🚦 Service Overview

### 🌐 Cloudflared (Ingress)
Creates a secure, outbound tunnel to Cloudflare’s Zero Trust network.  
> Configured via `cloudflare.config.netedge.yml`

### 🔁 Traefik (Reverse Proxy)
Handles routing and TLS termination for incoming requests.

- Uses **manually installed Cloudflare Origin Certificates (wildcard)** — _not_ Let's Encrypt  
- Configured via `traefik.netedge.yml` and `dynamic/` folder (optional)

### 🧱 Pi-hole (DNS + DHCP)
Network-wide DNS sinkhole and optional DHCP server.

- Connected to `casapilan` (macvlan) for LAN-level visibility  
- Admin UI: [http://192.168.1.24/admin/](http://192.168.1.24/admin/)

### 🧠 Unbound (Recursive DNS Resolver)
Private DNS upstream for Pi-hole, running on the same macvlan network.

---

## ⚙️ Prerequisites

- External Docker networks: `casaproxy`, `casapilan`  
- Static IPs reserved in your LAN for Pi-hole (`192.168.1.24`) and Unbound (`192.168.1.50`)  
- Cloudflare Origin Certificate + private key mounted to Traefik  

---

## 🔐 TLS with Cloudflare Origin Certificate

This stack uses a **Cloudflare Origin Certificate** for TLS, mounted directly into Traefik via Docker Compose.

Your `certs.yml` should look like:

```yaml
tls:
  stores:
    default:
      defaultCertificate:
        certFile: "/etc/traefik/certs/cloudflare-origin.pem"
        keyFile: "/etc/traefik/certs/cloudflare-origin.key"
  certificates:
    - certFile: "/etc/traefik/certs/cloudflare-origin.pem"
      keyFile: "/etc/traefik/certs/cloudflare-origin.key"
```

Mount this file in your `docker-compose-netedge.yml`:

```yaml
volumes:
  - /path/to/certs:/etc/traefik/certs
  - /path/to/certs.yml:/etc/traefik/dynamic/certs.yml
```

This avoids Let's Encrypt and ensures secure access via Cloudflare Tunnel.

Every exposed service is configured using Docker labels for Traefik. Example (for Ghost):

```yaml
labels:
  - traefik.http.routers.blog.rule=Host(`blog.chrisalmida.com`)
  - traefik.http.routers.blog.entrypoints=websecure
  - traefik.http.routers.blog.tls=true
```

---

## 🧑‍🔧 Macvlan Setup for `casapilan`

To allow containers like Pi-hole and Unbound to behave like separate devices on your LAN, this stack uses a macvlan network.

✅ Create the macvlan network manually:

```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  --ip-range=192.168.1.192/28 \
  -o parent=eth0 \
  casapilan
```

> 💡 **Note**: Replace `eth0` with your actual network interface (e.g., `enp3s0`, `ens18`). Run `ip a` to confirm.

### 🔒 Isolated from Host

Containers on a macvlan network **cannot communicate** with the Docker host by default. If you need API access (e.g., to Pi-hole), set up a proxy container **on a separate host**.

---

## 🚀 Deploy

```bash
docker compose -f docker-compose-netedge.yml up -d
```

---

## 🧰 Extras

- [Cloudflare Tunnel config reference](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/tunnel-guide/local/)  
- [Traefik documentation](https://doc.traefik.io/traefik/)  
- [Pi-hole + Unbound guide](https://docs.pi-hole.net/guides/dns/unbound/)  

---

## 🧼 Sanitization

All secrets, passwords, emails, tunnel IDs, and volume paths have been replaced with placeholders like:

```
ENTER_YOUR_CF_API_TOKEN_HERE
ENTER_YOUR_PIHOLE_PASSWORD_HERE
ENTER_YOUR_PWD_HERE
```

Replace these before deployment.

---

## 🧭 Credits

Created by [Chris Almida](https://sovereignliving.chrisalmida.com) as part of the Sovereign Self-Hosting series.

