# PAXECT Readiness Scanner FREE — Third-Party Software Notices

**Applies to:** PAXECT Readiness Scanner FREE, package `paxect-free` 0.1.0 (amd64, Ubuntu 24.04)
**Document status:** Final for release 0.1.0
**Last updated:** November 2026

## 1. Purpose

PAXECT Readiness Scanner FREE ("PAXECT FREE") uses independent open-source software. PAXECT acknowledges the authors and maintainers of these projects.

Each third-party component remains licensed under its own license. Nothing in the PAXECT FREE License Agreement restricts the rights you have under those licenses. The PAXECT FREE License Agreement applies only to PAXECT's own software.

The mention of a project or company name does not imply that its authors or owners sponsor, endorse, certify or support PAXECT.

## 2. Where to find the license texts

After installation, the complete, unmodified license and notice files are available locally at:

```
/usr/share/doc/paxect-free/THIRD_PARTY_NOTICES.md      (this document)
/usr/share/doc/paxect-free/third_party_licenses/       (original LICENSE / NOTICE files)
/usr/share/doc/paxect-free/third_party_licenses/SOURCES.json   (origin, version tag and SHA-256 of each file)
/usr/share/doc/paxect-free/copyright                   (Debian copyright summary)
/usr/share/doc/paxect-free/PAXECT_FREE_LICENSE_AGREEMENT.md   (license for PAXECT's own software)
/usr/share/doc/paxect-free/sbom/                       (SPDX inventory of the bundled Go binaries)
```

License texts of the bundled Python packages are additionally kept unmodified in their own `*.dist-info` directories under:

```
/usr/lib/paxect-free/tools/mcp/cisco-3.3.1-py312/lib/python3.12/site-packages/
```

## 3. Bundled scanner tools (redistributed in this package)

| Component | Version | Upstream project | License | Local files |
| --- | --- | --- | --- | --- |
| Syft | 1.43.0 | Anchore — github.com/anchore/syft | Apache-2.0 | `syft/LICENSE` |
| Trivy | 0.64.1 | Aqua Security — github.com/aquasecurity/trivy | Apache-2.0 | `trivy/LICENSE`, `trivy/NOTICE` |
| Grype | 0.97.1 | Anchore — github.com/anchore/grype | Apache-2.0 | `grype/LICENSE` |
| Gitleaks | 8.30.1 | Gitleaks contributors — github.com/gitleaks/gitleaks | MIT | `gitleaks/LICENSE` |
| Titus | 1.2.8 | Praetorian — github.com/praetorian-inc/titus | Apache-2.0 | `titus/LICENSE`, `titus/NOTICE` |
| Cisco AI Defense MCP Scanner | 3.3.1 | Cisco AI Defense — github.com/cisco-ai-defense/mcp-scanner | Apache-2.0 | `cisco-mcp-scanner/LICENSE` |

**Titus detection rules.** Titus includes detection rules derived from **Nosey Parker** (Praetorian) and **Kingfisher** (MongoDB). The applicable attribution is contained in the unmodified `titus/NOTICE` file.

**Trivy.** The unmodified `trivy/NOTICE` file is included.

**Cisco AI Defense MCP Scanner.** PAXECT FREE uses only the locally executed, offline static analysis. The open-source license of this project does not include access to any Cisco AI Defense hosted service, API, subscription or other paid offering. PAXECT FREE does not configure or use such services.

**Embedded Go modules.** Syft, Trivy, Grype, Gitleaks and Titus are distributed as statically linked Go binaries that contain further open-source Go modules (approximately 274, 381, 266, 64 and 136 modules respectively). These modules remain under their own licenses. A machine-readable inventory (SPDX SBOM, generated with the bundled Syft at build time) is installed per binary in `/usr/share/doc/paxect-free/sbom/`.

**Origin of the bundled binaries (verified November 2026).** Syft 1.43.0, Grype 0.97.1 and Titus 1.2.8 are the unmodified upstream linux/amd64 release binaries; their SHA-256 values match the checksum files published with the upstream GitHub releases. Trivy 0.64.1 is the unmodified upstream binary; because the original GitHub release assets are no longer available, it was verified byte-for-byte against the binary in the official `aquasec/trivy:0.64.1` container image. Gitleaks is built by PAXECT from the **unmodified** upstream source of release tag `v8.30.1` (commit `83d9cd684c87d95d656c1458ef04895a7f1cbd8e`) with Go 1.26.8, to include current Go standard-library security fixes; no source code was changed (build: `CGO_ENABLED=0 go build -trimpath -ldflags "-s -w -X github.com/zricethezav/gitleaks/v8/version.Version=8.30.1"`). PAXECT does not modify any of these programs.

## 4. Bundled Python packages (MCP route)

The Cisco AI Defense MCP Scanner runs with a bundled set of 82 Python packages. PAXECT does not modify these packages; they are included with their original license metadata and, where provided by the package, their license files. The package set was installed with pip from the Python Package Index (PyPI). The Cisco AI Defense MCP Scanner itself was installed from its PyPI wheel `cisco_ai_mcp_scanner-3.3.1-py3-none-any.whl`, verified against the SHA-256 digest published on PyPI; all 69 of its program files are byte-identical to that wheel. Every installed file of all 82 packages was verified against the package's own RECORD hashes (10,844 files, no deviations).

**License categories present:** MIT, MIT-0, BSD-2-Clause, BSD-3-Clause, Apache-2.0, ISC, PSF-2.0, CNRI-Python, MPL-2.0.

**Packages under the Mozilla Public License 2.0 (MPL-2.0):**

| Package | Version | License | Note |
| --- | --- | --- | --- |
| certifi | 2026.10.23 | MPL-2.0 | Distributed unmodified, in source form |
| tqdm | 4.70.1 | MPL-2.0 AND MIT | Distributed unmodified, in source form; license file added at `tqdm/LICENCE` |

The Source Code Form of these MPL-2.0 files is included in the package itself (Python source files). They are unmodified and remain available under the MPL-2.0 at https://mozilla.org/MPL/2.0/.

**Packages without an embedded license file**, for which the original license file has been added:

| Package | Version | License | Local file |
| --- | --- | --- | --- |
| tokenizers | 0.23.3 | Apache-2.0 | `tokenizers/LICENSE` |
| tqdm | 4.70.1 | MPL-2.0 AND MIT | `tqdm/LICENCE` |

**Compiled extensions.** Some packages contain compiled code that includes further third-party libraries under their own licenses, among others: `cryptography` (includes OpenSSL), `tokenizers`, `hf-xet`, `pydantic_core`, `jiter`, `rpds-py` and `tiktoken` (include Rust crates), and `yara-python` (includes the YARA library). These embedded libraries remain under their own licenses, as documented by the respective upstream package.

The complete list of the 82 packages, with versions and declared licenses, is reproduced in Annex A.

## 5. System components used but not distributed by PAXECT

The following software is installed by the Ubuntu package manager as a dependency of `paxect-free`. PAXECT does not redistribute it; it is provided by Ubuntu under its own licenses (see `/usr/share/doc/<package>/copyright`).

| Ubuntu package | Purpose in PAXECT FREE |
| --- | --- |
| python3 (3.12), python3-tk, python3-paramiko | Runtime, desktop interface, SSH/SFTP connector |
| bubblewrap | Isolation of firmware, APK and MCP analysis |
| squashfs-tools (GPL-2.0-or-later) | Extraction of SquashFS firmware filesystems (`/usr/bin/unsquashfs`, invoked as a separate program) |
| aapt, apksigner, openjdk-17-jre-headless | Android APK manifest decoding and signature verification |
| xdg-utils | Opening reports in the default browser |

## 6. Vulnerability databases and network connections by third-party components

On first use and periodically thereafter, Trivy and Grype download vulnerability databases from their upstream distribution services. These databases are **not** shipped with PAXECT FREE. They aggregate publicly available advisories from, among others, operating-system vendors, the National Vulnerability Database and the GitHub Advisory Database. Their contents and terms remain those of the respective database providers and data sources.

**Measured network connections (11 November 2026, system-call trace of the release components):**

- Trivy downloads its database from `mirror.gcr.io` (container image `aquasec/trivy-db`), over HTTPS;
- Grype downloads its database from `grype.anchore.io` (Anchore), over HTTPS;
- host names are resolved through the computer's normal DNS resolver;
- no update-check or telemetry connections were observed: PAXECT disables the self-update checks of Syft and Grype, and Trivy's database download made no other connection;
- during the analysis itself, the scanners run in a sandbox without network access; a monitored complete firmware scan made no internet connections at all;
- the MCP route runs without network access, and its bundled `litellm` package is configured to use only its local model price list.

No data from the scan input is sent in any of these connections.

Reports produced by PAXECT FREE may contain links to external advisory and guidance websites. Opening such a link connects to that website. PAXECT is not responsible for the content or availability of those websites.

## 7. Trademarks

Product and company names mentioned in this document, in the software or in reports are the property of their respective owners. They are used only to identify the corresponding software or data sources. No trademark rights are granted.

## 8. No warranty from upstream authors

The third-party software is provided by its authors under the terms of its licenses, including their disclaimers of warranty and limitations of liability. Upstream authors do not provide support for PAXECT FREE.

## 9. Contact

Questions about third-party components in PAXECT FREE: PAXECT-Team@outlook.com

---

## Annex A — Bundled Python packages (MCP route)

Declared license as recorded in each package's metadata at build time.

| Package | Version | Declared license |
| --- | --- | --- |
| aiohappyeyeballs | 2.7.1 | PSF-2.0 |
| aiohttp | 3.14.5 | Apache-2.0 AND MIT |
| aiosignal | 1.4.0 | Apache-2.0 |
| annotated-doc | 0.0.5 | MIT |
| annotated-types | 0.8.0 | MIT |
| anyio | 4.16.0 | MIT |
| attrs | 26.1.0 | MIT |
| boto3 | 1.43.124 | Apache-2.0 |
| botocore | 1.43.124 | Apache-2.0 |
| certifi | 2026.10.23 | MPL-2.0 |
| cffi | 2.1.1 | MIT-0 |
| charset-normalizer | 3.5.2 | MIT |
| cisco-ai-mcp-scanner | 3.3.1 | Apache-2.0 (upstream; no metadata field) |
| click | 8.5.0 | BSD-3-Clause |
| cryptography | 50.0.2 | Apache-2.0 OR BSD-3-Clause |
| expandvars | 1.1.2 | MIT |
| fastapi | 0.162.0 | MIT |
| fastuuid | 0.14.0 | BSD |
| filelock | 3.32.7 | MIT |
| frozenlist | 1.8.0 | Apache-2.0 |
| fsspec | 2026.9.0 | BSD-3-Clause |
| h11 | 0.16.0 | MIT |
| h2 | 4.4.1 | MIT |
| hf-xet | 1.8.0 | Apache-2.0 |
| hpack | 4.2.0 | MIT |
| httpcore | 1.0.9 | BSD-3-Clause |
| httpcore2 | 2.16.0 | BSD-3-Clause |
| httpx | 0.28.1 | BSD-3-Clause |
| httpx-sse | 0.4.3 | MIT |
| httpx2 | 2.16.0 | BSD-3-Clause |
| huggingface_hub | 1.33.0 | Apache-2.0 |
| hyperframe | 6.1.0 | MIT |
| idna | 3.20 | BSD-3-Clause |
| importlib_metadata | 8.9.0 | Apache-2.0 |
| Jinja2 | 3.1.6 | BSD |
| jiter | 0.18.0 | MIT |
| jmespath | 1.1.0 | MIT |
| jsonschema | 4.26.0 | MIT |
| jsonschema-specifications | 2025.9.1 | MIT |
| litellm | 1.108.0 | MIT (the separately licensed `enterprise/` directory is not included) |
| markdown-it-py | 4.2.0 | MIT |
| MarkupSafe | 3.0.4 | BSD-3-Clause |
| mcp | 1.30.0 | MIT |
| mdurl | 0.1.2 | MIT |
| multidict | 7.2.1 | Apache-2.0 |
| openai | 3.46.0 | Apache-2.0 |
| opentelemetry-api | 1.45.2 | Apache-2.0 |
| packaging | 26.3 | Apache-2.0 OR BSD-2-Clause |
| propcache | 0.5.4 | Apache-2.0 |
| pycparser | 3.12 | BSD-3-Clause |
| pydantic | 2.14.3 | MIT |
| pydantic-settings | 2.16.2 | MIT |
| pydantic_core | 2.50.4 | MIT |
| Pygments | 2.21.0 | BSD-2-Clause |
| PyJWT | 2.15.1 | MIT |
| python-dateutil | 2.9.0.post0 | Apache-2.0 / BSD (dual) |
| python-dotenv | 1.2.4 | BSD-3-Clause |
| python-multipart | 0.0.33 | Apache-2.0 |
| PyYAML | 6.0.3 | MIT |
| referencing | 0.37.0 | MIT |
| regex | 2026.9.29 | Apache-2.0 AND CNRI-Python |
| requests | 2.34.2 | Apache-2.0 |
| rich | 15.0.0 | MIT |
| rpds-py | 2026.9.1 | MIT |
| s3transfer | 0.19.3 | Apache-2.0 |
| shellingham | 1.5.4 | ISC |
| six | 1.17.0 | MIT |
| sniffio | 1.3.1 | MIT OR Apache-2.0 |
| sse-starlette | 3.6.0 | BSD-3-Clause |
| starlette | 1.10.0 | BSD-3-Clause |
| tiktoken | 0.14.0 | MIT |
| tokenizers | 0.23.3 | Apache-2.0 |
| tqdm | 4.70.1 | MPL-2.0 AND MIT |
| truststore | 0.10.5 | MIT |
| typer | 0.27.3 | MIT |
| typing-inspection | 0.4.5 | MIT |
| typing_extensions | 4.16.0 | PSF-2.0 |
| urllib3 | 2.8.0 | MIT |
| uvicorn | 0.54.0 | BSD-3-Clause |
| yara-python | 4.5.4 | Apache-2.0 |
| yarl | 1.25.1 | Apache-2.0 |
| zipp | 4.1.2 | MIT |

## 10. Artwork in the user interface

The desktop interface shows the following third-party artwork, pre-rendered as image files in
`/usr/lib/paxect-free/assets/1280/`. The artwork is used only to identify the corresponding input type.

| Artwork | Origin | License |
|---|---|---|
| Tux, the Linux penguin (`linux.rgba`) | Original by Larry Ewing, created with The GIMP; vector redraw by Garrett LeSage; refined by IFo Hancroft (github.com/garrett/Tux) | CC0 1.0 Universal (public domain dedication) |
| Android robot (`android.rgba`) | Google LLC (developer.android.com/distribute/tools/promote/brand) | Creative Commons Attribution 3.0 |
| Model Context Protocol logo (`mcp.rgba`) | Model Context Protocol project (modelcontextprotocol.io) | Property of its owner; shown only to identify MCP project input. No license is claimed. |

The Android robot is reproduced or modified from work created and shared by Google and used according
to terms described in the Creative Commons 3.0 Attribution License.

Linux is the registered trademark of Linus Torvalds in the U.S. and other countries. Android is a
trademark of Google LLC.

The PAXECT wordmark and the shield icon are original PAXECT artwork. The wordmark was rendered from the
DejaVu Sans Bold typeface; no font files are distributed.
