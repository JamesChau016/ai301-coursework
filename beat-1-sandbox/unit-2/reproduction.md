# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of the claim and reproduction for issue #62.

## Your identity upstream

**GitHub username**

JamesChau016

## Posted upstream

**Claim comment**

(https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62#issuecomment-5858288305)

I would like to investigate issue #62. The Redis probe in `api/routes/health.py` appears to read `settings.redis_host` and `settings.redis_port`, while `Settings` in `core/config.py` defines `redis_url` instead. I will set up the reproduction environment, confirm that Redis is reachable, and document the observed response and logs next. This investigation is AI-assisted; I used Claude Code to navigate the repository and draft this comment, and I will verify each command and result myself.

**Reproduction comment**

Not posted yet. Add the comment permalink here after posting it.

I reproduced the Redis health-check failure on the latest `main` at commit `f89c06f`.

**Environment**

- OS: Windows 10, version `10.0.19045`
- Python: `3.11.3`
- redis-py: `8.1.0`
- Redis: `7.4.9`, running in Docker
- PostgreSQL: `16`, running in Docker
- Application server: `uvicorn`
- AI assistance: Claude Code helped navigate the repository and draft this report; I ran and verified the commands and observations reported here.

**Steps**

1. Clone the repository and check out `f89c06f` (the latest `main` commit verified for this reproduction).
2. Create the repository environment and install its dependencies with `make setup`.
3. Start the backing services with `docker compose up -d db redis`.
4. Confirm that Redis is reachable: `docker exec <redis-container> redis-cli ping`. The command must return `PONG`.
5. Start the API with `uvicorn api.main:app --host 127.0.0.1 --port 8000`.
6. In a second terminal, call `curl -s -i http://127.0.0.1:8000/health`.

**Observed behavior**

Redis was reachable, but the health endpoint returned HTTP 503 and marked Redis unhealthy:

```text
$ docker exec pathreview-ai301-fa26-s1-redis-1 redis-cli ping
PONG

$ curl -s -i http://127.0.0.1:8000/health
HTTP/1.1 503 Service Unavailable
{"detail":{"status":"unhealthy","dependencies":{"postgres":"unhealthy","redis":"unhealthy","vector_db":"healthy"},"safety_events_last_hour":0,"timestamp":"2026-09-23T23:41:44.138541"}}
```

The corresponding application log identified the Redis-specific failure:

```text
redis_health_check_failed error="'Settings' object has no attribute 'redis_host'"
```

As a direct control, `settings.redis_url` was present and a Redis client created from that URL returned `ping: True`, while `has redis_host: False`. This shows that the probe fails while reading the nonexistent attribute, before it attempts the Redis connection. The `postgres` unhealthy result is a separate SQLAlchemy issue and is not evidence for this issue.

**Conclusion**

This reproduces issue #62. With Redis reachable, `/health` incorrectly reports Redis as unhealthy because `health_check()` reads `settings.redis_host` even though `Settings` provides `redis_url`.

## Eval iterations

**Run history**

19/20

**Package analysis**

`pkg-03`: my rubric decided `reject`, while the gold label was `accept`. The package contained the required reproduction evidence, but the grader reported `failed: env-recorded`. That disagreement shows that the environment section must state the exact operating-system version and runtime version explicitly rather than relying on a general platform description.

**Check rationale**

> Pass if the report explicitly specifies both the exact Operating System (with version) and the tool/software runtime version used during testing.

I kept this check because a reproduction cannot be independently evaluated when its environment is vague. I made the report explicit by recording Windows `10.0.19045`, Python `3.11.3`, redis-py `8.1.0`, Redis `7.4.9`, PostgreSQL `16`, and the tested commit `f89c06f`.

**Trade-offs**

Nothing changed elsewhere, and here is how I know: the final run recorded `categories: clear-accept 7/8 disclosure 1/1 no-evidence 4/4 unfollowable-comms 3/3 wrong-target 4/4` and `agreement: 19/20 scored items (bar: 18/20: PASS)`. The only disagreement was `pkg-03`, which failed `env-recorded`; the completed report addresses that specific gap without changing the other checks or their evidence.

Related paths: `eval-run.txt` in this directory; the installed skill files in `tools/repro-check/`.
