# Laptop Can't Reach the Local Network While VPN Is On

## Purpose
Restore access to the router and local devices when a VPN is routing local traffic into the tunnel.

## When to use it
- The laptop cannot ping the router or open its admin page.
- A phone or other device on the same Wi-Fi works fine.
- A VPN client (for example Tailscale) is installed on the laptop.

## Prerequisites
- Admin rights on the laptop.
- The router's IP address (`<ROUTER-IP>`).

## Steps
1. Confirm other devices on the same network can reach the router. If they cannot either, the router or network is down; this runbook does not apply.
2. Check the VPN status. Note whether it shows the subnet router as offline.
3. Check which path local traffic takes:
   - Linux: `ip route get <ROUTER-IP>`
   - Windows: `route print`
4. If the route goes out the VPN interface (for example `tailscale0`) instead of the Wi-Fi or Ethernet interface, the VPN is sending local traffic into the tunnel.
5. Stop the VPN from accepting subnet routes while on the home network:
   - `sudo tailscale set --accept-routes=false`
   - or `sudo tailscale down` to turn the VPN off temporarily.
6. Re-run the route check from step 3.

## Verify
- `ip route get <ROUTER-IP>` now shows the local interface.
- Ping to the router succeeds and the admin page loads.

## Escalate if
- The route already uses the local interface but the router is still unreachable (possible router, cable or Wi-Fi fault).

## Prevention
- Turn route acceptance off at home and on only when away.
