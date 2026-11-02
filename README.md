# Python Job Board Discovery and Matching

A read-only Python toolkit for collecting job listings from Greenhouse, Lever, and Ashby and comparing them with a supplied skills list. It normalizes public job data, checks freshness and location rules, and returns explainable match results.

## Features

- Fetch public listings from three applicant tracking systems and normalize their fields.
- Parse publication times and compensation when a source supplies them; follow Lever pagination.
- Score a supplied set of technical skills and explain eligibility checks.
- Limit network destinations, redirects, retries, and concurrent requests.
- Run mocked tests without accounts, credentials, or live network access.

This is a reusable extraction from a larger personal job-search project. It does not submit applications or include personal profiles, résumés, or application history.

## Get started

Requires Python 3.11 or newer.

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m src --help
```

Use a public board identifier from the provider's job-board URL:

```sh
python -m src greenhouse BOARD_ID --company "Company name" --limit 20
python -m src lever BOARD_ID --skill Python --skill SQL
python -m src ashby BOARD_ID --skill TypeScript
```

Output is JSON. Supplying `--skill` adds a match result for each job; without it, the command only discovers listings. These commands make read-only requests to the provider's public API.

## Matching scope

The included policy is designed around India-compatible or worldwide remote engineering roles. It checks publication age, role, location, experience, and known salary ceilings before scoring skills. Missing dates or ambiguous locations can lead to rejection. The score is a heuristic, not an ATS score or a hiring prediction; review the returned reasons alongside the original posting.

## Tests

```sh
pip install -r requirements-dev.txt
python -m pytest -q
```

Tests use synthetic listings and mocked HTTP responses. No browser, résumé, or account is needed.
