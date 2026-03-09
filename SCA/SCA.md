# Software Composition Analysis (SCA)
SCA is a security practice that identifies vulnerabilities, license risks, and outdated dependencies in open-source components used by your application.
# Why SCA Matters
When you build an app, you pull in dozens (sometimes hundreds) of third-party libraries. SCA answers:

Are any of these libraries vulnerable (CVEs)?
Are licenses compliant with your org's policy?
Are packages outdated or unmaintained?


# SCA for Python with pip-audit
pip-audit is the most popular SCA tool for Python. It scans your dependencies against the OSV (Open Source Vulnerabilities) and PyPI Advisory databases.
1. Installation
```bash
pip install pip-audit
```
2. Basic Usage
## Scan current environment
```sh
pip-audit
```
## Scan a requirements file
```sh
pip-audit -r requirements.txt
```
## Scan a specific package
```sh
pip-audit --package requests==2.20.0
```

3. Output Formats
## JSON output (great for CI/CD parsing)
```sh
pip-audit -r requirements.txt -f json -o audit-results.json
```

## Markdown output
```sh
pip-audit -r requirements.txt -f markdown
```

## Cyclone DX SBOM (Software Bill of Materials)
```sh
pip-audit -r requirements.txt -f cyclonedx-json
```
4. Auto-fix Vulnerabilities
## Automatically upgrade vulnerable packages
```sh
pip-audit -r requirements.txt --fix
```

## Dry-run (shows what would be fixed)
```sh
pip-audit -r requirements.txt --fix --dry-run
```

5. CI/CD Integration (GitHub Actions)
## .github/workflows/sca.yml
name: SCA Security Scan
```sh
on: [push, pull_request]

jobs:
  sca:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run pip-audit
        run: |
          pip install pip-audit
          pip-audit -r requirements.txt -f json -o audit-results.json

      - name: Upload audit results
        uses: actions/upload-artifact@v3
        with:
          name: sca-audit-results
          path: audit-results.json
```

6. Pre-commit Hook
```yaml
.pre-commit-config.yaml
repos:
  - repo: https://github.com/pypa/pip-audit
    rev: v2.6.1
    hooks:
      - id: pip-audit
        args: ["-r", "requirements.txt"]
```
> Note: bandit is actually SAST (Static Application Security Testing), not SCA — but they're often used together.


Full Security Pipeline Example
## 1. SCA - Check dependencies for CVEs
```sh
pip-audit -r requirements.txt
```
## 2. SAST - Check your own code
```sh
pip install bandit
bandit -r ./src -f json -o bandit-results.json
```

## 3. License compliance check
```sh
pip install pip-licenses
pip-licenses --format=markdown --with-urls
```

## 4. Generate SBOM
```sh
pip install cyclonedx-bom
cyclonedx-py -r -i requirements.txt -o sbom.json
```