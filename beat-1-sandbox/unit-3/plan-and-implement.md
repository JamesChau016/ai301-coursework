# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

JamesChau016

**Plan comment**

(https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62#issuecomment-5986158101)

I plan to fix issue #62 by correcting the Redis health probe's configuration
lookup. The reproduced failure shows that Redis is reachable (`redis-cli ping`
returns `PONG`), but `health_check()` reads `settings.redis_host` before it can
connect. `Settings` defines `redis_url` instead, so the probe raises
`AttributeError` and `/health` reports Redis as unhealthy.

I will make the smallest fix in `api/routes/health.py`: update the Redis
client construction in `health_check()` to use `settings.redis_url`, the
existing configuration field, while preserving the current health response and
logging behavior. I will inspect `core/config.py` to confirm the field and its
type, but I will not add a second setting, change the Redis service, alter the
PostgreSQL or vector-database checks, upgrade dependencies, or broaden the
health endpoint.

To verify the change, I will repeat the reproduction against the same
environment: start `db` and `redis`, confirm `PONG`, run Uvicorn, and call
`curl -s -i http://127.0.0.1:8000/health`. The Redis-specific log
`redis_health_check_failed error="'Settings' object has no attribute
'redis_host'"` must no longer occur, and the response's
`dependencies.redis` value must be `healthy` while Redis is reachable. I will
also add or run a focused automated health-check test that supplies a
`redis_url` and verifies the Redis probe calls that URL successfully; it must
fail before the change because the implementation reads `redis_host` and pass
afterward. This investigation and plan were AI-assisted with Claude Code; I
will verify the implementation and test results myself.

---

## Your branch

**Branch**

fix/62-redis-health-check

**Evidence**

Before the fix, on commit `f89c06f`, I ran:

```text
docker compose up -d db redis
docker exec pathreview-ai301-fa26-s1-redis-1 redis-cli ping
PONG

uvicorn api.main:app --host 127.0.0.1 --port 8000
curl -s -i http://127.0.0.1:8000/health
HTTP/1.1 503 Service Unavailable
{"detail":{"status":"unhealthy","dependencies":{"postgres":"unhealthy","redis":"unhealthy","vector_db":"healthy"},"safety_events_last_hour":0,"timestamp":"2026-09-23T23:41:44.138541"}}

redis_health_check_failed error="'Settings' object has no attribute 'redis_host'"
```

The direct control also showed `settings.redis_url` was present, a Redis
client created from that URL returned `ping: True`, and `has redis_host: False`.

After the fix, I will repeat the same commands on
`fix/62-redis-health-check`:

```text
docker compose up -d db redis
docker exec pathreview-ai301-fa26-s1-redis-1 redis-cli ping
PONG

uvicorn api.main:app --host 127.0.0.1 --port 8000
curl -s -i http://127.0.0.1:8000/health
HTTP/1.1 503 Service Unavailable
```

The post-fix response must report
`"dependencies":{"redis":"healthy"}` and the application log must contain no
`Settings`/`redis_host` AttributeError. The overall status may remain 503
because PostgreSQL may remain unhealthy; that is the separate SQLAlchemy issue
identified in the reproduction and is not part of this fix.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- 20/20

**Package analysis**

`pkg-02`: rubric decision = accept; gold label = accept. The package was
accepted because the plan identifies the reproduced cause, limits the change
to the Redis configuration lookup, and gives concrete before/after checks
using the health endpoint and Redis reachability. The decision agrees with the
gold label.

**Check rationale**

I used the `diagnosis` check exactly as written:

> Passes if the plan states a specific cause that explains what the repro evidence shows AND its planned change fixes that cause; fails if it only restates the symptom, states a cause the evidence contradicts, or plans a workaround/safety net (docs note, catch-all recover, retry) instead of fixing the cause

This check keeps the plan grounded in the reproduction: Redis responds to
`PING`, while the probe fails earlier when it reads the nonexistent
`settings.redis_host`. The planned change uses the existing
`settings.redis_url`; it does not hide the AttributeError with a catch-all,
retry, or documentation-only workaround.

**Trade-offs**

Nothing changed elsewhere, and here is how I know: the final run recorded
`categories: clear-accept 7/7 scope-creep 4/4 thread-convention 2/2 unbuildable 3/3 wrong-cause 4/4`
and `agreement: 20/20 scored items (bar: 18/20: PASS)`. The plan deliberately
leaves the separate PostgreSQL failure, dependency versions, service
configuration, and unrelated health checks unchanged.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
