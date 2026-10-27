# Server Unreachable ("No route to host"): Lost Static IP

## Purpose
Find and fix a server that is running but no longer has its expected static IP address.

## When to use it
- A script or user gets "No route to host" or cannot ping the server's usual address.
- The server is powered on (check the hypervisor or console).
- This often follows a power outage or reboot.

## Prerequisites
- Console access to the server (not only SSH, because the address may be wrong).
- Admin (sudo) rights.
- The server's expected IP address (`<SERVER-IP>`).

## Steps
1. From another machine, ping `<SERVER-IP>`. If it fails, continue.
2. Open the server's console and run `ip -br addr`. Compare the address to what is expected. A different address means it fell back to DHCP.
3. List the network config files: `ls /etc/netplan/`. Netplan merges every `.yaml` file, so more than one file can conflict.
4. Open each file and check:
   - the interface name matches the real one from `ip -br addr` (for example `ens18`, not `eth0`)
   - `dhcp4: false` is set for the static interface
   - DNS server entries are plain IPs with no `/24`
5. Back up the files, for example `sudo cp /etc/netplan/<file>.yaml /root/<file>.yaml.bak`.
6. Keep one correct file (static address, default route, DNS) and remove the conflicting one.
7. Validate the syntax: `sudo netplan generate`.
8. Apply it: `sudo netplan apply`. An SSH session may drop; reconnect to `<SERVER-IP>`.

## Verify
- `ip -br addr` shows `<SERVER-IP>` on the correct interface.
- Ping from another machine succeeds.
- Reboot the server and confirm the address is still correct.

## Escalate if
- The address and config are correct but the server is still unreachable (check the switch, router, VLAN or DHCP reservation).

## Prevention
- Verify the live address after any network change.
- Consider a DHCP reservation in the router as a backup.
