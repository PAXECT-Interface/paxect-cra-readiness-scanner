# PAXECT CRA Readiness Scanner FREE

**Free local readiness scanner for the EU Cyber Resilience Act (CRA).**

**No account. No cloud. No telemetry.** · [Download the latest release](../../releases/latest) · [Install and verify](#install) · [Security policy](SECURITY.md)

PAXECT CRA Readiness Scanner FREE helps manufacturers of products with digital elements see where their product stands ahead of the main obligations of the CRA, which apply from 11 December 2027. It scans firmware, Linux systems, Android apps and MCP server projects **on your own Ubuntu computer** and produces a clear HTML technical report with the findings and the evidence behind them, including a software bill of materials (SBOM) and known vulnerabilities where the input type allows it.

> **Free to use, not open source.** PAXECT FREE is distributed free of charge as an Ubuntu package with a signed checksum file, under the [PAXECT FREE License Agreement](LICENSE.md). This repository contains documentation and release files only; the source code of PAXECT itself is not published. The bundled open-source components keep their own licenses — see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

**Your scan input is not uploaded anywhere.** It is analysed on your own computer inside an isolated sandbox without network access. Network access is only used to download public vulnerability databases and, for the SSH / SFTP input type, to read the device you choose to scan.

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

In the Files app, open the folder with the four files, right-click an empty area and choose **Open in Terminal**. Then run:

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

gpg may also warn that the key is not certified with a trusted signature. That is normal for a newly imported key. The signature only counts if the fingerprint in step 1 matched: that check confirms the key is the one PAXECT published here. Because the fingerprint is published in the same place as the key, you can also confirm it with PAXECT through a second channel (see About below).

```bash
# 3. Install (apt also installs the required Ubuntu packages)
sudo apt update
sudo apt install ./paxect-free_0.1.0_amd64.deb
```

Start **PAXECT FREE** from the application menu, or run `paxect-free` in a terminal.

The first scan also downloads the vulnerability databases and can take a few minutes. Later scans are faster.

## Update

Download the new release files and verify them as above. Then install the new package; replace `<new-version>` with the version in the file name you downloaded:

```bash
sudo apt update
sudo apt install ./paxect-free_<new-version>_amd64.deb
```

Your earlier reports are kept.

## Uninstall

```bash
sudo apt remove paxect-free
```

Your reports and downloaded databases stay in `~/.local/share/paxect-free/`. Delete that folder yourself if you no longer need them. Reports you saved to another location are not affected.

## Privacy and security

- **Local only.** There is no account, no cloud service and no telemetry from PAXECT. Scan input is not uploaded anywhere.
- **Sandboxed analysis.** The bundled scanners run in a [bubblewrap](https://github.com/containers/bubblewrap) sandbox: no network access during analysis and the scan input is mounted read-only.
- **Network use.** Network access is only used to download public vulnerability databases (Trivy from `mirror.gcr.io`, Grype from `grype.anchore.io`) and, for the SSH / SFTP input type, to read the device you choose to scan. Nothing from your scan input is sent. Measured details are in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md), section 6.
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
Yes, where the input type allows it. For firmware images, PAXECT FREE builds a software bill of materials (SBOM) of the scanned product and uses it to find known vulnerabilities; the report shows both. Reports for other input types contain the findings that apply to them, for example static security analysis and secret detection for MCP projects.

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
