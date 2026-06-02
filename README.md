# ThreatLens AI

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](#requirements)
[![Status](https://img.shields.io/badge/status-MVP-green)](#status)
[![Security](https://img.shields.io/badge/security-defensive%20lab-purple)](#safe-use)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

AI-style log investigation assistant. Parses Linux auth logs, nginx access logs, and Docker container logs, then highlights suspicious IPs, exposed secrets, and produces a structured incident summary.

---

## Overview

ThreatLens AI is a defensive analysis tool that ingests common log formats and produces an investigation-style report. It parses Linux `auth.log`, nginx access logs, and Docker container logs, correlates suspicious IPs, flags accidentally logged secrets, and assembles a Markdown incident report ready for analyst review.

The current MVP is a Python CLI. A FastAPI + React web dashboard is scaffolded under `apps/` for future development.

## Features

- Parses Linux auth logs, nginx access logs, and Docker container logs
- Identifies suspicious source IPs across log types
- Flags exposed secrets accidentally logged
- Correlates events into incidents
- Generates AI-style incident summary explanations
- Outputs JSON findings, incident summary, Markdown report, and triage handoff

## Requirements

- Python 3.10 or newer
- Linux, macOS, or Windows
- No third-party Python packages (standard library only)
- Optional: Docker for the demo container

## Installation

```bash
git clone https://github.com/SUDARSHANCHAUDHARI/ThreatLensAI.git
cd ThreatLensAI
pip install .
```

This registers the `threat-lens` CLI command.

To run without installing:

```bash
python3 main.py --help
```

## Usage

Analyze the included sample log bundle:

```bash
python3 main.py analyze --fixture data/samples/log-bundle.json --out-dir data/reports
```

Generated outputs in `data/reports/`:

- `events.json` — parsed log events
- `findings.json` — flagged suspicious activity and secrets
- `incident.json` — correlated incident summary
- `summary.json` — counts and severity breakdown
- `report.md` — Markdown incident report
- `triage.md` — analyst triage checklist

## Project Structure

```
ThreatLensAI/
├── apps/
│   ├── api/        FastAPI app scaffold (planned)
│   └── web/        React/Next.js dashboard scaffold (planned)
├── data/
│   ├── samples/    Safe sample log bundles
│   └── reports/    Example generated output
├── docker/         Dockerfile + compose support
├── docs/           Architecture, security notes, demo
├── scripts/        Setup, seed, run helpers
├── tests/          Unit and integration tests
├── main.py         CLI entrypoint
├── pyproject.toml  Package metadata
└── LICENSE
```

## Testing

```bash
python3 -m unittest discover -s tests -p 'test_*.py'
```

## Docker Demo

```bash
docker compose run --rm api
```

## Safe Use

This project is defensive and analysis-focused. Use only with logs and lab environments you own or have explicit written permission to assess. The included sample logs are synthetic and safe for public demo use.

## Status

Working Python CLI MVP. Web dashboard scaffold present but not yet implemented.

## Roadmap

- Real LLM integration for incident summarization
- Additional log format support (Kubernetes, syslog, cloud audit logs)
- Live log streaming mode
- Web dashboard with incident timeline visualization
- GitHub release `v0.1.0-mvp`

## License

Released under the [MIT License](LICENSE). You are free to use, modify, and distribute this software with attribution.

## Author

**Sudarshan Chaudhari** — [SudarshanTechLabs](https://github.com/SUDARSHANCHAUDHARI)
Bangkok, Thailand

For inquiries: open an issue on [GitHub](https://github.com/SUDARSHANCHAUDHARI/ThreatLensAI/issues).
