# Domain Join Fails: "The Domain Could Not Be Contacted"

## Purpose
Fix a PC that cannot join the Active Directory domain even though it has network connectivity.

## When to use it
- The domain join shows "the domain could not be contacted."
- Pinging the domain controller's IP address works.

## Prerequisites
- Administrator rights on the PC.
- The domain controller's IP address (`<DC-IP>`).
- The domain name (for example `corp.example.local`).

## Steps
1. Ping the domain controller's IP: `ping <DC-IP>`. If it fails, this is a network problem, not DNS; use the network troubleshooting runbook instead.
2. Open the PC's network adapter settings and check the preferred DNS server.
3. If it points to the router or any public DNS server, change it to `<DC-IP>`.
4. Confirm the PC can resolve the domain name: `nslookup <domain-name>`. It should return the domain controller's address.
5. Retry the domain join.

## Verify
- The join completes and the PC asks for a restart.
- After restart, a domain account can sign in.

## Escalate if
- The DNS setting is already correct but the join still fails. Check that the DNS service is running on the domain controller.

## Prevention
- Add "set DNS to the domain controller" to the new-PC checklist.
