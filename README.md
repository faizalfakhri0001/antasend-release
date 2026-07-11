# API Pilot artifact-only release control

This directory is the complete non-source payload for `faizalfakhri0001/api-pilot-release`.
It contains only the verification/deployment workflow, its JSON contract, and the deployer
public key. Do not add application source, migration SQL, shell scripts from the application,
environment files, or Vercel pull output.

Bootstrap it explicitly (this command writes to the separate origin3 worktree, never the
source repository):

```bash
rtk bash scripts/sync-origin3-control-repo.sh --gpg-key <fingerprint>
```

Review and push that worktree separately. Configure the `production` environment on origin3
with reviewers and the VPS runner before dispatching a release. Frontend Vercel credentials and
prebuilt output stay on the deployer's workstation.
