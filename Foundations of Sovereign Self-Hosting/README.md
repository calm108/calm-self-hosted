## calm-self-hosted/Foundations of Sovereign Self-Hosting (Series)

# Foundations of Sovereign Self-Hosting

A five-part educational series by [Chris Almida](https://blog.chrisalmida.com), teaching you how to build your own media server and homelab using Docker, open-source apps, and privacy-first principles.

---

## 📌 Purpose
This series provides a **modular, real-world guide** to setting up your own sovereign self-hosted stack. Ideal for:
- Digital minimalists
- Homesteaders
- Privacy advocates
- Tech-aware entrepreneurs
- Anyone who wants full control of their digital environment

Each part includes:
- A working `docker-compose.yml`
- Commentary and setup instructions
- Real-world context based on my own homelab

---

## 📚 Series Overview

| Part | Topic | Blog Link | Docker Compose File Link
|------|-------|-------------------|
| 1 | Setting Up the Media Server Environment | [Part 1](https://blog.chrisalmida.com/foundations-of-sovereign-self-hosting/) | [Compose Base] (./Media Server Stack/docker-compose.yml)
| 2 | Media Players (Plex, Jellyfin, Navidrome, Audiobookshelf, Mealie) | [Part 2](https://blog.chrisalmida.com/part-2-media-players-the-heart-of-your-system/) | [Compose Part 2] (./Media Server Stack/docker-compose-part-2.yml)
| 3 | Media Management (*Arr apps) | [Part 3]() |
| 4 | Downloading & Indexing | [Part 4]() |
| 5 | Requests & Analytics | [Part 5]() |

---

## 🛠 Prerequisites
- Ubuntu or Unraid host
- Basic familiarity with Docker
- Static IP config preferred
- `casaproxy`, `casavpn`, `casalan`, `casapilan` external networks (defined outside Compose)

---

## ⚙️ Customization
You are expected to clone and edit each Compose file based on your network, volumes, and desired media paths. Comments in each file will guide you.

Trash Guides and other community resources are referenced where applicable.

---

## 🧠 Philosophy
> "Run what you own, own what you run."

No cloud lock-in. Minimal external dependencies. Secure by default.

---

## 📬 Questions or Contributions
Pull requests and feedback welcome. 
Connect with Chris at:
-[https://blog.chrisalmida.com](https://blog.chrisalmida.com).
-[@soverignalmida](https://x.com/sovereignalmida)
