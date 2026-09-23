# Intentionally outdated items

Approximate "first safe version" pointers for instructor reference. Confirm with
a scanner (npm audit, pip-audit, Trivy, OSV) since advisory data evolves.

## npm (api/)
| Package | Pinned | Known issue class | Fixed in (approx.) |
|---|---|---|---|
| lodash | 4.17.4 | Prototype pollution (merge/defaultsDeep) | 4.17.21 |
| minimist | 1.2.0 | Prototype pollution | 1.2.6+ |
| jsonwebtoken | 8.2.0 | Signature/algorithm validation weaknesses | 9.0.0 |
| axios | 0.18.0 | SSRF / ReDoS | 0.21.2+ / 1.x |
| moment | 2.19.1 | ReDoS | 2.29.4 |
| handlebars | 4.0.11 | Prototype access / RCE | 4.7.7 |
| ejs | 2.5.7 | Template injection | 3.1.10 |
| js-yaml | 3.10.0 | Code execution via unsafe load | 3.13.1+ |
| node-fetch | 2.6.0 | Header leak on redirect | 2.6.7 |
| mongoose | 5.0.10 | Prototype pollution / injection | 5.13+ / 6.x |
| serialize-javascript | 1.5.0 | XSS/RCE via serialization | 3.1.0+ |
| express / body-parser | 4.16.0 / 1.18.2 | Multiple advisories | 4.21+ / 1.20+ |

## pip (worker/)
| Package | Pinned | Known issue class | Fixed in (approx.) |
|---|---|---|---|
| Flask | 0.12.2 | DoS via crafted JSON | 0.12.3 / 2.x |
| Jinja2 | 2.10 | Sandbox escape | 2.10.1 / 3.1.x |
| Werkzeug | 0.14.1 | Debugger / DoS issues | 0.15.x / 3.x |
| PyYAML | 3.12 | Arbitrary code exec via `yaml.load` | 5.4+ (use `safe_load`) |
| requests | 2.19.1 | Credential leak on redirect | 2.20.0+ |
| urllib3 | 1.22 | Multiple CRLF / cert / DoS issues | 1.26.x+ |
| Pillow | 5.2.0 | Many memory-safety CVEs | 10.x |
| cryptography | 2.1.4 | Timing / padding issues | 3.3+ |
| paramiko | 2.4.0 | Auth bypass | 2.4.2+ |
| SQLAlchemy | 1.2.0 | SQL injection via order_by/group_by | 1.2.18+ |
| gunicorn | 19.7.1 | HTTP request smuggling | 20.x+ |

## Runtime / platform EOL
- Node.js 8, npm 5 - EOL
- Python 3.6 - EOL
- MongoDB 3.6 - EOL
- Docker Compose file format v2, Travis CI config

## Legacy code smells to discuss
- `var` + callbacks in `server.js`; no async/await
- `_.merge` on untrusted request bodies
- 7-day JWT with static secret from env default
- `yaml.load` without a Loader; `render_template_string`
