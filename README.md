# Prime Mover (WordPress) — CVE Writeups

Three vulnerabilities I discovered in the **Prime Mover** WordPress migration plugin
through source code review, reproduced in an isolated local lab, and responsibly
disclosed to the vendor. All are **fixed in 2.2.1** and I am **credited in the
changelog**.

| CVE | Class | Severity (CVSS 4.0) |
|---|---|---|
| [CVE-2026-101888](CVE-2026-101888-prime-mover-zip-slip/) | Zip Slip → arbitrary file write (CWE-22) | High — 8.6 |
| [CVE-2026-101889](CVE-2026-101889-prime-mover-path-traversal/) | Path traversal → arbitrary directory deletion (CWE-22) | High — 7.0 |
| [CVE-2026-101890](CVE-2026-101890-prime-mover-stored-xss/) | Stored XSS via package metadata (CWE-79) | Medium — 5.1 |

## Approach

1. **Source review** — trace archive/package input from the import entry points to the
   file, delete, and output sinks.
2. **Lab reproduction** — version-matched WordPress in Docker, reproduced end to end.
3. **Impact proof** — demonstrate file write / directory deletion / script execution.
4. **Disclosure** — report privately, verify the fix against 2.2.1.

## Responsible use

Published **after** the fix shipped. The PoC builders use **benign marker payloads**
(harmless canary strings / `alert(document.domain)`), not drop-in webshells — the goal
is to explain the root cause and the fix, not to arm attackers. All testing was done
only in my own authorized local lab.

## Contact

Sarvar Eshboyev — eshsarvar@gmail.com — [LinkedIn](https://www.linkedin.com/in/sarvar-eshboyev)
