# Continuous Integration & Security Pipeline with GitHub Actions

This repository features a robust, production-grade **CI/CD pipeline** implemented with GitHub Actions. It integrates modern best practices for **code quality assurance**, **security vulnerability scanning**, and **containerized deployment** — showcasing advanced DevOps and DevSecOps skills.

---

## Pipeline Overview

### Primary Workflow: `ci.yml`

- **Trigger:** Automatically runs on every push or pull request to the `main` branch
- **Key Stages:**
  - **Secret Scanning** via [Gitleaks](https://github.com/gitleaks/gitleaks) to prevent sensitive data leaks
  - **Vulnerability Assessment** using [Trivy](https://github.com/aquasecurity/trivy) on the filesystem/dependencies
  - **Static Code Analysis** powered by [SonarCloud](https://sonarcloud.io/) for code quality, coverage, and maintainability
  - **Docker Image Build & Push** leveraging Docker Buildx for multi-platform support and publishing to Docker Hub

---

### Secondary Workflow: `owasp-manual.yml`

- **Trigger:** Executed manually through the GitHub Actions UI (`workflow_dispatch`)
- **Purpose:** Comprehensive dependency vulnerability scanning using [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
- **Benefit:** Offloads heavier security scans from the primary pipeline, allowing on-demand detailed auditing without slowing down core CI runs
- **Output:** HTML vulnerability report uploaded as a downloadable artifact for detailed review

---

## Visual Pipeline Flow

```mermaid
graph TD
  A[Push / PR to main] --> B[Gitleaks - Secret Scan]
  B --> C[Trivy - Vulnerability Scan]
  C --> D[SonarCloud - Static Analysis]
  D --> E[Docker Build & Push]
