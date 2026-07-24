# Security Policy

## Supported versions

The table below shows which versions of this project currently receive security updates.

| Version | Supported          |
|---------|--------------------|
| latest  | :white_check_mark: |
| < latest| :x:                |

We recommend always using the latest release. Security fixes are not backported to older versions unless explicitly noted.

## Reporting a vulnerability

**Do not open a public issue for security vulnerabilities.** Public disclosure before a fix is available puts all users at risk.

### How to report

Send a detailed report to **[security@example.com](mailto:security@example.com)** (replace with your actual contact address) or use GitHub's private vulnerability reporting feature if enabled for this repository.

Include the following information in your report:

- **Description**: What is the vulnerability? How can it be exploited?
- **Impact**: What can an attacker achieve? Who is affected?
- **Steps to reproduce**: Provide a minimal, reproducible example or proof of concept.
- **Environment**: Affected versions, operating system, runtime version if applicable.
- **Suggested fix**: If you have a patch or mitigation, include it (optional).

### What to expect

- **Acknowledgement**: You will receive a confirmation within **48 hours**.
- **Assessment**: We will investigate and confirm the issue within **7 days**.
- **Fix timeline**: Security fixes are prioritised. We aim to release a patch within **30 days** for critical issues, **60 days** for high-severity issues.
- **Disclosure**: Once a fix is released, we will publish a security advisory. If you request it, we will credit you in the advisory.

### Scope

This security policy applies to the code in this repository. It does not cover:

- Vulnerabilities in third-party dependencies (report those to the upstream maintainer)
- Issues in infrastructure or deployment environments not controlled by this project
- Social engineering or phishing attacks

If you are unsure whether an issue qualifies as a security vulnerability, report it anyway. We will assess it and redirect you if it belongs elsewhere.

## Security best practices

When using this project:

- Always run the latest released version.
- Review release notes and changelogs for security-related updates.
- Follow the principle of least privilege — do not grant more permissions than necessary.
- If deploying this project, ensure the environment is hardened (firewall rules, up-to-date OS, secure configuration).

## Past security advisories

Security advisories for this project are published in the [GitHub Security Advisories](https://github.com/Kuroshitsuji/REPO_NAME/security/advisories) section.

If no advisories are listed, no security issues have been disclosed to date.
