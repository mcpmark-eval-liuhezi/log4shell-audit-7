# Security Notes: Log4Shell — CVE-2021-44228

Prepared for the lab quarterly security briefing. Facts below are pulled from primary sources; exact version numbers and the CVSS score are stated because they will be presented to the group.

## What Log4Shell is
A JNDI lookup feature used in Apache Log4j2 configurations, log messages, and message parameters does not protect against attacker-controlled LDAP and other JNDI related endpoints. An attacker who can control log messages or log message parameters can execute arbitrary code loaded from LDAP servers.

Only the `log4j-core` JAR is impacted. Applications using only `log4j-api` (without `log4j-core`) are not impacted.

## CVE id
**CVE-2021-44228**

## Severity
**CVSS 3.x Score: 10.0 — CRITICAL**
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H

## Affected versions (Log4j 2)
`[2.0-beta9, 2.3.1) ∪ [2.4, 2.12.2) ∪ [2.13.0, 2.15.0)`

Equivalently: **all Log4j 2.x from 2.0-beta9 through 2.14.1**.

## Fixed versions
| Platform | Fixed version |
| --- | --- |
| Java 8 and later | **2.15.0** |
| Java 7 | 2.12.2 (backport) |
| Java 6 | 2.3.1 (backport) |

## Related Log4Shell-family CVEs and fixes
| CVE | CVSS | Affects | Fixed in |
| --- | --- | --- | --- |
| CVE-2021-45046 | 9.0 critical | JNDI RCE in certain non-default configurations | 2.16.0 |
| CVE-2021-45105 | 5.9 medium | Inf recursive lookup / DoS | 2.17.0 |
| CVE-2021-44832 | arbitrary code execution | JDBCAppender; requires write access to config | 2.17.1 |

## Recommended production target
**2.17.1** (Java 8+), 2.12.4 (Java 7), 2.3.2 (Java 6) — the final patched line covering the whole Log4Shell family in one upgrade.

## Remediation actions tracked
1. Uppgrade to patched Log4j versions (see issue #2)
2. Disable attacker-controlled JNDI lookups — JndiLookup must not be loaded (see issue #3)
3. Detect vulnerable deployments by `log4j-core` version per Java tier (see issue #4)
4. Automated dependency scanning of `log4j-core` in every build pipeline (see issue #5)

## Sources
- Apache Logging Services — Security: https://logging.apache.org/security.html
- NVD — CVE-2021-44228: https://nvd.nist.gov/vuln/detail/CVE-2021-44228
- GitHub Advisory Database — GHSA-jfh8-c2jp-5v3q: https://github.com/advisories/ghsa-jfh8-c2jp-5v3q
- Apache Software Foundation — Apache Log4j CVEs: https://news.apache.org/foundation/entry/apache-log4j-cves

*Created 2026-10-29. Working copy of the findings behind the security log4shell-audit-7 repo.*
