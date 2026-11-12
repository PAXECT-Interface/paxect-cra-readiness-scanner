# Security Policy

## Reporting a vulnerability

If you find a security issue in PAXECT CRA Readiness Scanner FREE, please report it privately:

- **E-mail:** PAXECT-Team@outlook.com
- **Subject:** `SECURITY: PAXECT FREE <short description>`

Please do **not** open a public GitHub issue for security problems.

Include, where possible:

- the PAXECT FREE version (`apt policy paxect-free`) and your Ubuntu version;
- what you did, what happened and what you expected;
- steps to reproduce, or a proof of concept;
- whether the issue is already known publicly.

Do not include real customer data, secrets or firmware you are not allowed to share.

## What to expect

- We aim to acknowledge your report within **5 working days**.
- We will keep you informed while we investigate and fix the issue.
- Fixed versions are published as signed releases on this page. With your permission, we credit you in the release notes.

## Supported versions

| Version | Supported |
| --- | --- |
| 0.1.x (latest release) | Yes |
| Earlier test builds | No |

## Verifying releases

All releases are signed with the PAXECT release signing key:

```
PAXECT Release Signing <PAXECT-Team@outlook.com>
Fingerprint: F914 7E2E C87B B514 BCA5  D9F7 0C18 1E6D 1CFD B2A9
```

Install only packages whose `SHA256SUMS` file has a good signature from this key. See the installation steps in the [README](README.md#install).

## Bundled third-party components

PAXECT FREE bundles open-source scanners (Syft, Grype, Trivy, Gitleaks, Titus, Cisco AI Defense MCP Scanner). Vulnerabilities in those projects should also be reported to their maintainers. We update the bundled versions in new PAXECT FREE releases.
