# Sigma Forge

## Description
**Sigma Forge** is a Detection-as-Code repository containing a collection of vendor-agnostic detection rules (Sigma + YARA) mapped to the MITRE ATT&CK framework. It is built as a portfolio project demonstrating threat research, detection engineering, and automated testing capabilities.

## Architecture
- **Rules**: Written in Sigma for behavioral detections, and YARA for static artifacts.
- **Hypothesis/Hunting**: Each technique includes a `hunt.md` file documenting the hypothesis, data sources, and triage steps.
- **Testing**: Python-based automated tests validate logic against synthetic benign log data (JSON) and safely crafted test files.
- **Conversion**: Sigma rules are automatically translated into Splunk SPL and Microsoft Sentinel KQL via Python scripts (`pysigma`).
- **CI/CD**: GitHub Actions validate all rules and run tests on every push and pull request.

## Workflow
Research ➔ Hunt Doc ➔ Sigma Rule ➔ Convert to SPL/KQL ➔ YARA ➔ Tests ➔ CI Pipeline

## Quick Start
1. Clone the repository.
2. Create a virtual environment: `python -m venv venv`
3. Install requirements: `pip install -r requirements.txt`
4. Run build script to generate KQL/SPL: `python scripts/build.py`
5. Run tests: `pytest`

## Limitations
- **Synthetic Data**: Tests are executed against synthetic log events and benign strings (like EICAR). No real malware or exploit code is included in this repository.
- **Untested in Production**: The converted queries have not been executed or tuned against live Splunk or Sentinel production environments.
- **Tuning Required**: All rules must be evaluated and tuned against real environment telemetry before production deployment to reduce false positives.
