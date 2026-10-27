# IT Helpdesk Runbooks

Step-by-step troubleshooting runbooks written from real incidents in my home lab, which includes a Windows Server Active Directory domain, Ubuntu servers, and a private VPN. Each runbook covers one problem: the symptoms, the steps to fix it, how to verify, and when to escalate.

## Runbooks

| Runbook | What it fixes |
| --- | --- |
| [Domain join fails with "domain could not be contacted"](runbooks/domain-join-fails-dns.md) | A PC can reach the domain controller but cannot join the domain, caused by the wrong DNS server |
| [VPN blocks access to the local network](runbooks/vpn-blocks-local-network.md) | A laptop cannot reach the router or local devices because the VPN is routing local traffic into the tunnel |
| [Server unreachable: lost static IP](runbooks/server-lost-static-ip.md) | A server is running but unreachable because it fell back to DHCP after a netplan misconfiguration |

## How each runbook is written

- **Purpose** and **When to use it**: the problem and its symptoms
- **Prerequisites**: access and information needed
- **Steps**: numbered, one action per step
- **Verify**: how to confirm the fix worked
- **Escalate if**: when to hand it to the next tier

## About

Open to IT support and systems roles.

Contact: [https://www.linkedin.com/in/harrison-stamps]

All IP addresses and names in these runbooks are placeholders.
