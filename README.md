## sovereign-self-hosted (Main Repository)

# sovereign-self-hosted

A curated, real-world stack of self-hosted applications and homelab infrastructure by [Chris Almida](https://sovereign.chrisalmida.com), focused on **sovereignty, privacy, and decentralization**.

This repo contains the full architecture, Docker Compose files, and configuration notes used in my personal sovereign tech environment, built around:

- **Docker Compose** for container orchestration
- **Traefik** for dynamic reverse proxy + TLS
- **Unraid** and **Ubuntu** as host environments
- **Self-sovereign infrastructure**: Pi-hole, Immich, Cal.com, Vikunja, Audiobookshelf, Nextcloud, etc.
- **Ansible** for future automated deployment (WIP)

---

## 📚 Series: [Foundations of Sovereign Self-Hosting](./Foundations%20of%20Sovereign%20Self-Hosting)

This educational series walks through the process of building a complete media server + homelab environment, step-by-step, using free and open source software (FOSS). Each part includes a real Docker Compose file reflecting a tested stack.

| Part | Topic |
|------|-------|
| 1 | Setting Up the Media Server Environment |
| 2 | Media Players (Plex, Jellyfin, Navidrome, Audiobookshelf, and Mealie) |
| 3 | Media Management (Arr apps: Radarr, Sonarr, Lidarr, Readarr, Bazarr) |
| 4 | Downloading & Indexing (Prowlarr, qBittorrent, SABnzbd, MeTube) |
| 5 | Requests & Analytics (Overseerr, Radarec, Sonashow, Tautulli) |

---

## 🛠 Tech Stack Highlights

- `docker compose` syntax (no version key)
- Uses named stacks and custom external networks (e.g., `casaproxy`, `casavpn`)
- Network isolation and DNS control via Pi-hole + macvlan
- Cal.com integration with Ghost blog (WIP)
- Manual TLS via Cloudflare Origin Certificates

---

## 📂 Repo Structure

```
sovereign-self-hosted/
├── Foundations of Sovereign Self-Hosting/
│   ├── Part-1-Environment/
│   ├── Part-2-Players/
│   ├── Part-3-Managers/
│   ├── Part-4-Downloaders/
│   ├── Part-3-Requests-Analytics/
├── Ansible/                   # WIP automation
├── Compose-Stacks/            # Modular stacks
|   ├── NetworkEdge Stack      # Modular Network Edge stack with Cloudflare and Traefik
└── README.md                  # This file
```

## 🔐 Philosophy
This project is about **owning your tools**, **controlling your data**, and opting out of cloud dependencies where possible.

Join the journey or fork and remix it for your needs. Feedback and pull requests welcome.

---

## 📫 Contact
Chris Almida
Blog: [https://sovereign.chrisalmida.com](https://sovereign.chrisalmida.com)  
X: [@sovereignalmida](https://x.com/sovereignalmida)
