# Detection-as-Code (DaC) with Sigma, GitHub Actions, ELK & Wazuh

[![CI/CD Pipeline](https://github.com/your-org/detection-as-code/actions/workflows/detection-pipeline.yml/badge.svg)](https://github.com/your-org/detection-as-code/actions/workflows/detection-pipeline.yml)

## Overview

This repository implements **Detection-as-Code (DaC)** – treating security detection rules as software code. It provides a complete workflow for authoring, validating, and deploying detection rules using:

- **Sigma** – vendor‑neutral rule format (YAML)
- **GitHub** – version control, pull requests, branch protection
- **GitHub Actions** – CI/CD pipeline with validation, conversion, and deployment
- **Elastic Security (ELK)** – SIEM rule management via Kibana API
- **Wazuh** – endpoint detection and response (EDR) with XML rules

The pipeline automatically validates every rule change, converts Sigma rules to platform‑specific formats (EQL for Elastic, XML for Wazuh), and deploys them to production SIEM environments after peer review and automated checks.

---

## Key Benefits

- **Version control** – full history, blame, rollback
- **Peer review** – mandatory pull request approvals
- **Automated validation** – YAML syntax, Sigma schema, structural tests, and unit tests
- **Continuous deployment** – rules pushed to ELK and Wazuh automatically
- **Governance** – branch protection, approval gates, signed commits
- **Consistency** – single source of truth, no configuration drift
- **Audit readiness** – immutable change log for compliance (SOC2, ISO27001, NIST)

---

## Architecture

![DaC Architecture](docs/architecture.png)

The pipeline consists of three layers:

1. **Authoring** – Engineers write Sigma rules in `rules/` on feature branches.
2. **Validation & Governance** – GitHub Actions runs YAML lint, Sigma schema validation, structural checks, and unit tests. Pull requests require at least one approval and passing status checks.
3. **Deployment** – Validated rules are converted to EQL (Elastic) and XML (Wazuh), then deployed to Elastic Security (via API) and staged for Wazuh (SSH/file copy). A production approval gate adds human oversight.

---

