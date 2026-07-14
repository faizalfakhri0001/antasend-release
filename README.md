# API Pilot artifact-only release control

This directory is the complete non-source payload for `faizalfakhri0001/antasend-release`.
It contains only the verification/deployment workflow, its JSON contract, the deployer
public key, and the versioned VPS environment-patch helper. Do not add application source,
migration SQL, environment files, or Vercel pull output.

Run `Update production deployment helper` after a reviewed change to
`scripts/apipilot-apply-deployment-env`, before publishing a release that uses a newly
managed backend environment key. The job requires the same `production` approval as a backend
release and verifies the installed helper checksum. If the runner sudoers policy does not permit
the helper installation, set `VPS_SUDO_PASSWORD` as a temporary `production` environment secret,
run the workflow, then delete the secret after the checksum is confirmed.

Bootstrap it explicitly (this command writes to the separate origin3 worktree, never the
source repository):

```bash
rtk bash scripts/sync-origin3-control-repo.sh --gpg-key <fingerprint>
```

Review and push that worktree separately. Configure the `production` environment on origin3
with reviewers and the VPS runner before dispatching a release. Frontend Vercel credentials and
prebuilt output stay on the deployer's workstation.
