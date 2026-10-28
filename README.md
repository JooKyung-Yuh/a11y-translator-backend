# A11y Translator — Backend

Django REST API for URL-based accessibility scanning (axe-core) and comments.
Current state: project skeleton only. No endpoint is implemented yet.

## Setup

Requires Python 3.10+.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt
python backend/manage.py migrate
python backend/manage.py runserver
```

## Structure

| Path | Owns |
|---|---|
| `backend/config/` | settings, root URLs |
| `backend/scans/` | S1–S5 (accessibility scan) |
| `backend/comments/` | C1–C4 (comments) |

## API

| # | Method | Path | Description |
|---|---|---|---|
| S1 | POST | `/api/scans/` | Request a scan for a URL |
| S2 | GET | `/api/scans/{scan_id}/` | Scan status + overall summary |
| S3 | GET | `/api/scans/{scan_id}/issues/` | Issue list (`status`, `impact`, `rule_id` filters) |
| S4 | GET | `/api/scans/{scan_id}/issues/{issue_id}/` | Issue detail |
| S5 | GET | `/api/scans/{scan_id}/screenshot/` | Full-page screenshot (PNG) for the viewer |
| C1 | GET | `/api/scans/{scan_id}/comments/` | List comments (`issue_id` filter) |
| C2 | POST | `/api/scans/{scan_id}/comments/` | Create comment |
| C3 | PATCH | `/api/comments/{comment_id}/` | Edit comment |
| C4 | DELETE | `/api/comments/{comment_id}/` | Delete comment |

Full field-level spec lives in the team Notion page.

## Notes

- `SECRET_KEY` in `config/settings.py` is the generated dev key. Do not use it in production.
- Not in scope yet: login, scan worker (Playwright + axe-core), AI explanations, sharing.
