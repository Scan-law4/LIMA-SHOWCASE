# Assets & Subscriptions Inventory — 2026-04-07

## Owner
**Name**: Scan
**Location**: Zagreb, Croatia
**System**: Local AI Workstation (fully owned, no cloud dependencies)
**Built**: 2024–2025 (Aurus Xtreme platform, custom assembly/upgrade)

---

## Hardware — Internal (Main Machine)

### GPU: NVIDIA GeForce RTX 3090
- **Platform**: Aurus Xtreme (not custom-cooled, 3 fans)
- **VRAM**: 24GB GDDR6X
- **Firmware**: Updated end of 2025
- **Usage**: Local inference, model serving

### CPU
- **Model**: AMD Ryzen 7 5700X3D
- **Cores**: 8 cores, 16 threads
- **Base**: 3.0 GHz | **Boost**: 4.4 GHz
- **Cache**: 96MB 3D V-Cache
- **Temp**: ~67°C idle, ~80–85°C under load

### Motherboard
- **Model**: B550 AORUS Elite AX V2
- **WiFi**: 802.11ac + BT 5.0
- **Ethernet**: 2.5GbE (dual LAN)

### RAM
- **Kit**: Corsair Vengeance RGB PRO
- **Capacity**: 128 GB (4x 32GB)
- **Speed**: 3200 MHz DDR4
- **Usage**: ~104 GB available

### Storage
- **System**: Crucial P510 1TB NVMe (root /)
- **Free**: 504 GB
- **Note**: Single disk — no dedicated data volume

### Additional Storage
- **Secondary**: 907 GB NVMe (unified with system partition)
- **Total Internal**: ~1.9 TB

### External Devices
| Device | Capacity/Spec | Purpose |
|--------|--|---------|
| Meta Quest 3 | 128 GB | VR, prototyping, visualization |
| Xiaomi Redmi Note 9 Pro | 128 GB | AI testing, edge AI, mobile experiments |
| Revopoint Metro X | N/A | 3D scanning, metrology |
| + | — | — |

---

## Subscriptions — Current (Auto-Renewal Tracking)

### 1. Cursor AI — Pro Plan
- **Cost**: $20/mo
- **Includes**: Premium models, unlimited tabs, advanced AI features
- **Renewal**: Apr 2, 2026 → May 2, 2026 (current billing cycle)
- **Status**: Active (will expire May 2, 2026)
- **Usage**: Local-first, but Cursor useful for complex tasks
- **Goal**: Transition away as local models improve
- **Action**: May 2 — decide whether to renew

### 2. Claude AI — Pro Plan
- **Cost**: ~$20/mo (estimate)
- **Renewal**: Apr 28, 2026
- **Includes**: Opus model, complex planning, troubleshooting
- **Usage**: When local models hit limits, for architecture/planning
- **Status**: Active, auto-renews
- **Note**: Keep for occasional tasks; goal is local-only workflow

### 3. SuperGrok — Research Plan
- **Cost**: ~$30/mo (estimate)
- **Renewal**: Apr 21, 2026
- **Includes**: Web research, Twitter/X scraping, graphics, animation
- **Usage**: Web updates, real-time info, media generation
- **Status**: Active, auto-renews
- **Goal**: Keep for cutting-edge research (not critical)

### 4. ISP — Croatian A1
- **Plan**: Small Business (unlimited speed, unlimited data)
- **Lines**: 2 numbers (Scan personal + AI) (Note: likely wrong number in prompt, should be 1 or business line)
- **Cost**: Flat rate, unlimited download/upload
- **Connection**: Fiber/GPON (fastest available in Croatia)
- **Notes**: Dedicated internet for AI workloads

### 5. Other (TBD)
- **GitHub**: Free or Pro? (Need to check)
- **Cloudflare**: Free or Pro plan?
- **Vercel/Netlify**: Free or paid?
- **Check Later**: Are there other subs?

---

## Maintenance Schedule

### Daily
- Check disk usage
- Monitor GPU temp (nvidia-smi)
- Review error logs

### Weekly (Sunday)
- Run health check script: `~/.hermes/maintenance/check_health.sh`
- Update packages: `sudo apt update && sudo apt upgrade -y`
- Check subscription renewals due within 7 days
- Backup critical files (if needed)

### Monthly
- Review subscription usage
- Decide whether to renew/let lapse
- Update hardware firmware (GPU, BIOS if applicable)
- Prune Ollama cache if disk >80%

### Quarterly
- Full system audit
- Backup verification
- Model retraining/optimization review
- External device maintenance (Quest 3, scanner)

---

## Notes
- This inventory grows as I discover new components/subscriptions
- Ask me to add/remove entries
- Track subscription expiration dates closely
- Goal: Reduce dependency on paid subs (Cursor, Claude, SuperGrok)
- Priority: Local-first, but keep critical tools until alternatives exist

---

*Last updated: 2026-04-07*