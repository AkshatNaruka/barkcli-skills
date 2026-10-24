---
id: oauth-rotation
name: OAuth Secret Rotation
description: Rotate OAuth client secrets with zero downtime
triggers: [oauth, secret, token, rotation]
---
# OAuth Secret Rotation

1. **Add before remove.** Register the new secret as a second credential;
   only delete the old one after every consumer has migrated.
2. ** consumers first.** Sweep logs for who still uses the old secret —
   scheduled jobs and webhooks are the usual stragglers.
3. **Fail closed in staging.** Prove the new secret rejects the old token
   flow before flipping production.
4. **Record the rotation.** Store the new secret expiry in the vault entry
   so the next rotation is scheduled, not discovered.
