# DHCP Threat Hunting Dashboard Using Splunk

---

##  Overview

This project focused on building a DHCP threat hunting dashboard using Splunk and Zeek DHCP logs.

The objective was to improve visibility into DHCP behavior, lease activity, and client-server relationships through operational dashboarding.

---

##  Objective

To develop a visual dashboard for DHCP monitoring, behavioral analysis, and threat hunting workflows within a SOC lab environment.

---

##  Lab Setup

- **Log Source:** Zeek (`dhcp.log`)
- **SIEM:** Splunk
- **Environment:** Virtual Lab (Kali Linux + VirtualBox)

---

##  Dashboard Panels

### 1. DHCP Lease Distribution

Visualized DHCP lease assignments by DHCP server.

```spl
index=main sourcetype=zeek_dhcp
| rex field=_raw "(?<server_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by server_ip
| sort - count
```

Visualization Type:
- Bar Chart

---

### 2. Top DHCP Clients

Displayed the most active DHCP clients within the environment.

```spl
index=main sourcetype=zeek_dhcp
| rex field=_raw "(?<client_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by client_ip
| sort - count
| head 10
```

Visualization Type:
- Column Chart

---

### 3. DHCP Behavioral Consistency

Validated whether clients communicated with multiple DHCP servers.

```spl
index=main sourcetype=zeek_dhcp
| rex field=_raw "(?<client_ip>\d+\.\d+\.\d+\.\d+).*?(?<server_ip>\d+\.\d+\.\d+\.\d+)"
| stats dc(server_ip) as server_count by client_ip
```

Visualization Type:
- Table

---

##  Analysis & Findings

The dashboard provided operational visibility into:

- DHCP lease activity
- Client behavior patterns
- DHCP infrastructure consistency
- Behavioral baselining

Observed behavior showed stable DHCP relationships across the environment.

---

##  Dashboard Screenshot

![DHCP Threat Hunting Dashboard](./dhcp_dashboard.png)

---

##  SOC Insight

Dashboards enhance SOC operations by transforming raw telemetry into actionable operational intelligence.

Visualization improves analyst efficiency, accelerates investigations, and strengthens anomaly detection workflows.

---

##  Key Takeaway

Effective detection engineering requires both strong analytics and strong visibility engineering.

Operational dashboards improve threat hunting capability by making network behavior easier to monitor and analyze.

---

##  Next Steps

- Integrate DNS telemetry into dashboarding workflows
- Develop alert-driven threat hunting dashboards
- Expand Zeek log correlation analysis

---

##  Tags

`Splunk` `Dashboarding` `Threat Hunting` `Detection Engineering` `SOC Analyst` `DHCP`
