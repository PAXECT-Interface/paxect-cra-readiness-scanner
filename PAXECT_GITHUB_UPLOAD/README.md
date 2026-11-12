# PAXECT CRA Readiness Scanner FREE

**Free local readiness scanner for the EU Cyber Resilience Act (CRA).**

**No account. No cloud. No telemetry.** · [Download v0.1.0](../../releases/latest) · [Install and verify](#install) · [Security policy](SECURITY.md)

PAXECT CRA Readiness Scanner FREE helps manufacturers of products with digital elements see where their product stands before the CRA obligations apply. It scans firmware, Linux systems, Android apps and MCP server projects **on your own Ubuntu computer** and produces a clear HTML technical report with a software bill of materials (SBOM) and known vulnerabilities.

> **Free to use, not open source.** PAXECT FREE is distributed free of charge as a signed Ubuntu package under the [PAXECT FREE License Agreement](LICENSE.md). This repository contains documentation and release files only; the source code of PAXECT itself is not published. The bundled open-source components keep their own licenses — see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

**Your files never leave your computer.** Scan input is analysed inside an isolated sandbox without network access. Only public vulnerability databases are downloaded.

---

## What it scans

| Input | What PAXECT FREE does |
| --- | --- |
| **Firmware file** | Extracts the SquashFS file system in an isolated sandbox, builds an SBOM and matches it against known vulnerabilities. |
| **Linux system (folder)** | Scans an extracted Linux root file system. |
| **Linux system (SSH / SFTP)** | Reads the file system of a device you are authorised to access and scans it locally. |
| **Android APK** | Checks the manifest, signatures, security settings and bundled components. |
| **MCP project** | Static security analysis of a Model Context Protocol server project, including secret detection. |

The result is one HTML report per scan, with the evidence it is based on, which you can save, share and archive.

## Requirements

- **Ubuntu 24.04 LTS** (desktop), 64-bit (amd64)
- Internet access for installation and for downloading the public vulnerability databases
- Other Ubuntu versions and distributions are not supported in this release

## Install

Download these four files from the [latest release](../../releases/latest) into one folder:

- `paxect-free_0.1.0_amd64.deb`
- `SHA256SUMS`
- `SHA256SUMS.asc`
- `PAXECT_RELEASE_SIGNING_KEY.asc`

Open a terminal in that folder and run:

```bash
# 1. Import the PAXECT release signing key and show its fingerprint
gpg --import PAXECT_RELEASE_SIGNING_KEY.asc
gpg --fingerprint PAXECT-Team@outlook.com
```

**Check that the fingerprint is exactly:**

```
F914 7E2E C87B B514 BCA5  D9F7 0C18 1E6D 1CFD B2A9
```

Stop if it differs.

```bash
# 2. Verify the signature and the package checksum
gpg --verify SHA256SUMS.asc SHA256SUMS      # must say: Good signature from "PAXECT Release Signing"
sha256sum -c SHA256SUMS                     # must say: paxect-free_0.1.0_amd64.deb: OK
```

gpg may also warn that the key is not certified with a trusted signature. That is normal for a newly imported key: the fingerprint check in step 1 is what proves the key is genuine.

```bash
# 3. Install (apt also installs the required Ubuntu packages)
sudo apt update
sudo apt install ./paxect-free_0.1.0_amd64.deb
```

Start **PAXECT FREE** from the application menu, or run `paxect-free` in a terminal.

The first scan also downloads the vulnerability databases and can take a few minutes. Later scans are faster.

## Update

Download the new release files, verify them as above, then:

```bash
sudo apt update
sudo apt install ./paxect-free_<new-version>_amd64.deb
```

Your earlier reports are kept.

## Uninstall

```bash
sudo apt remove paxect-free
```

Your reports and downloaded databases stay in `~/.local/share/paxect-free/`. Delete that folder yourself if you no longer need them.

## Privacy and security

- **Local only.** There is no account, no cloud service and no telemetry from PAXECT. Scan input is not uploaded anywhere.
- **Sandboxed analysis.** The bundled scanners run in a [bubblewrap](https://github.com/containers/bubblewrap) sandbox: no network access during analysis, scan input read-only, no access to your home folder.
- **Network use.** Network access is only used to download public vulnerability databases: Trivy from `mirror.gcr.io`, Grype from `grype.anchore.io`. Nothing from your scan input is sent. Measured details are in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md), section 6.
- **Signed releases.** The checksum file (`SHA256SUMS`) of every release is signed with the PAXECT release key (fingerprint above); it covers the package checksum.
- **Verified components.** The bundled scanner binaries were verified against their official upstream releases.

To report a security issue, see [SECURITY.md](SECURITY.md).

## Limitations

- **Readiness, not certification.** PAXECT FREE shows technical findings that are relevant for CRA readiness. It does **not** certify a product, does not make a product compliant, and is not legal advice. Conformity assessment under the CRA remains the responsibility of the manufacturer.
- Findings come from automated tools and public databases. They can contain false positives and cannot find every issue.
- Firmware support in this release: images that contain a SquashFS file system.
- Only scan products and systems you own or are authorised to test.

## Frequently asked questions

**What is the EU Cyber Resilience Act (CRA)?**
Regulation (EU) 2024/2847 sets cybersecurity requirements for products with digital elements sold in the EU. Reporting obligations for actively exploited vulnerabilities apply from 11 September 2026; the main obligations apply from 11 December 2027.

**Is there a free Cyber Resilience Act (CRA) readiness scanner that runs locally?**
Yes — PAXECT CRA Readiness Scanner FREE runs entirely on your own Ubuntu computer, without an account or cloud upload.

**Does PAXECT FREE create an SBOM?**
Yes. Each scan builds a software bill of materials of the scanned product and uses it to find known vulnerabilities. The report shows both.

**Does PAXECT FREE make my product compliant with the Cyber Resilience Act?**
No. It is a readiness tool: it helps you find and document technical issues early. Compliance requires a full conformity assessment.

**Can I use PAXECT FREE in my business?**
Yes. You may use it free of charge for private and business purposes, including assessments for your own customers. Selling, redistributing or offering it as a hosted service requires written permission. See the [PAXECT FREE License Agreement](LICENSE.md).

## About

PAXECT CRA Readiness Scanner FREE is made by **Vincent Simon (PAXECT Lab)**, the Netherlands.

- Website: [paxect.eu](https://paxect.eu)
- LinkedIn: [linkedin.com/in/vincent-simon-paxect](https://www.linkedin.com/in/vincent-simon-paxect)
- E-mail: PAXECT-Team@outlook.com

Product and company names mentioned here are the property of their respective owners.
