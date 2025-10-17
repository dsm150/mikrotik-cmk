# MikroTik API Agent for Checkmk (CRE)

Custom **Datasource Program** for **Checkmk Raw Edition** that polls **MikroTik RouterOS 7** via **classic API (8728)** using `librouteros`, and outputs:

- System metrics: CPU, Memory (+ perfdata)
- Interfaces: state (running/disabled)
- **WAN checks** via `/tool/ping interface=<iface> address=<target>`
  - local checks: `wan_MainGW`, `wan_RsrvGW`, `wan_LastChanceGW`
  - aggregated local check: `wan_overall` (CRIT if **only** LastChanceGW is up)

> **No SNMP required.** Works as a **special agent / datasource program**.

---

## Features

- 🚫 **No SNMP** — only RouterOS API (8728/8729)
- 🧠 Robust RTT parser (`18ms384us`, `00:00:00.050`, `1s234ms`, etc.)
- 📡 WAN via specified interfaces (policy-routing agnostic)
- 🟢 Local checks with perfdata (graphs in CRE)
- 🧰 Easy to extend: add speeds, errors/drops, PPPoE/BGP/OSPF, etc.

---

## Requirements

- Checkmk **Raw Edition (CRE)** on Linux
- RouterOS **7.x** (classic API enabled)
- Python3 on site user
- `librouteros` installed into the **site** Python path

---

## Installation (on Checkmk server)

> Replace `monitoring` with your site name if different.

```bash
# become site user
sudo -i
omd su monitoring

# 1) Install librouteros into site-local path
pip3 install --upgrade pip
pip3 install librouteros --target $OMD_ROOT/local/lib/python3

# 2) Place agent
mkdir -p ~/local/share/check_mk/agents/special
cp agents/special/agent_mikrotik ~/local/share/check_mk/agents/special/agent_mikrotik
chmod +x ~/local/share/check_mk/agents/special/agent_mikrotik
