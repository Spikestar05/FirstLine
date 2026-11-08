# Flood relaunch progress

Goal: restart the agent worker with today's fixes, redeploy the site with the narrowed flood zone, relaunch the flood on the 43 riverbank homes only, and report how the agents did.

## Log

- 2026-11-08 11:17 CST — Step 0: created this file on branch `ops/flood-relaunch` (from `origin/main`).
- 2026-11-08 11:17 CST — Step 1 (access check): **FAILED, stopping here.** The cloud session that ran this has neither access:
  - **SSH to root@207.148.5.196: missing.** No `ssh` client is installed in the container and there is no SSH private key (no usable `~/.ssh`). The worker cannot be started and the site cannot be redeployed from here.
  - **`spacetime` CLI logged in as the owner of Maincloud `firstline`: missing.** The `spacetime` binary is not installed and there is no SpacetimeDB login/identity in the container, so `spacetime sql --server maincloud firstline ...` and owner-only reducers (`mark_safe`, `check_in`) cannot run.
  - Also noted: `web/.env.production.local` is not present in this checkout (git-ignored), so step 3 would have been skipped anyway.
  - Nothing was changed on Vultr or Maincloud. State is as the previous session left it: worker STOPPED, site not redeployed, the 239-household flood still open (239 needs_help, 239 open SOS).

## To resume

Run steps 2–8 from a machine that has the Vultr SSH key and `spacetime login` as the database owner (for example the laptop used for earlier deploys), or give a cloud environment those credentials through its environment settings (not in chat).
