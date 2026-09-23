# TaskMaster-API (legacy)

A deliberately **aging** cloud service used as a realistic target for dependency
management, software composition analysis (SCA), and upgrade-planning exercises.

> ⚠️ Do NOT deploy this to a public network. It pins old, known-vulnerable
> package versions on purpose. Run it only in an isolated lab.

## Architecture

| Component | Stack | Path |
|-----------|-------|------|
| REST API  | Node.js 8 / Express 4.16 | `api/` |
| Worker    | Python 3.6 / Flask 0.12  | `worker/` |
| Datastore | MongoDB 3.6 (docker-compose) | - |

The API accepts tasks (`/tasks`) and hands reminder/report jobs to the worker
(`/jobs`), which renders templates and posts to a webhook.

## Quick start (lab only)

```bash
docker-compose up --build
curl localhost:3000/health
curl localhost:5000/health
```

## Suggested exercises

1. Run `npm audit` in `api/` and `pip-audit -r worker/requirements.txt` (or
   `safety check`, OWASP Dependency-Check, Trivy, Grype) and record findings.
2. Build an inventory / SBOM (`cyclonedx-npm`, `cyclonedx-py`, or `syft`).
3. Triage: which findings are reachable from the code in `api/src` and `worker/`?
4. Plan the upgrade: which bumps are patch/minor/major? What breaks?
5. Fix the runtime EOLs (Node 8, Python 3.6, Mongo 3.6) and update the Dockerfiles.
6. Add a CI gate that fails on high/critical findings.

See `docs/LEGACY_NOTES.md` for the intentionally outdated items and the
version that fixes each. Verify current advisories with your scanner; the
database changes over time.
