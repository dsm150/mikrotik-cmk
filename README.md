# MikroTik API Agent for Checkmk (CRE)
Custom **Datasource Program** for **Checkmk Raw Edition** that polls **MikroTik RouterOS 7** via **classic API (8728)** using `librouteros`, and outputs:
- System metrics: CPU, Memory (+ perfdata)
- Interfaces: state (running/disabled)
- WAN checks via `/tool/ping interface=<iface> address=<target>`
  - local checks: `wan_MainGW`, `wan_RsrvGW`, `wan_LastChanceGW`
  - aggregated local check: `wan_overall` (CRIT if **only** LastChanceGW is up)

> **No SNMP required.** Works as a **special agent / datasource program**.

## Installation
... (truncated for brevity; see ChatGPT full content)
