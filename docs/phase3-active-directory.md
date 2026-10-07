# Phase 3 — Active Directory buildout

**Goal:** promote the Windows Server to a Domain Controller and get the
endpoint joined to the resulting domain.

Before starting, confirm the DC can reach the Splunk server
(`ping 192.168.10.10`).

## Promote the server

1. **Server Manager → Manage → Add Roles and Features** → role-based
   install → check **Active Directory Domain Services** → install.
2. Click the post-install notification flag → **Promote this server to a
   domain controller**.
3. Choose **Add a new forest**, set the root domain name to
   **`varun.local`**, provide a DSRM password, and let it restart.

## Build out users and OUs

Under **Server Manager → Tools → Active Directory Users and Computers**,
expand the domain and create:

- An OU (e.g. **IT**) containing a test user with login name of your
  choosing, password set, "must change password at next logon" unchecked.
- A second OU (e.g. **HR**) with a second test user, same settings.

> Screenshot suggestions: the source archive does not include Phase 3 screenshot files.
At this point `varun.local` is a functioning domain.

## Join the endpoint

1. On the target machine: **This PC → Properties → Advanced system settings
   → Computer Name → Change** → domain → `varun.local`. An error here is
   expected on the first attempt — don't close the dialog.
2. Point the endpoint's DNS at the DC's IP (`192.168.10.7`) via the network
   adapter settings, then verify with `ipconfig /all`.
3. Retry the domain join, authenticating with the DC's local administrator
   account, then restart.
4. At the sign-in screen, choose **Other user**, confirm *Sign in to* shows
   `varun.local`, and log in with one of the domain accounts created above.
The endpoint is now a member of `varun.local` and authenticating against the
domain controller.

---
➡️ Next: [Phase 4 — Attack simulation and detection](phase4-attack-and-detection.md)
