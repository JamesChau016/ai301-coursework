# Plan for issue #62: Redis health-check configuration

## Diagnosis

The Redis service is reachable: `docker exec <redis-container> redis-cli ping`
returns `PONG`. However, `health_check()` in `api/routes/health.py` attempts to
read `settings.redis_host` before it connects. That attribute does not exist on
`Settings`; `core/config.py` provides `redis_url` instead. The resulting
`AttributeError` causes the health endpoint to mark Redis unhealthy even though
the connection is available.

## Scope

1. Confirm the existing `redis_url` field and its type in `core/config.py`.
2. In `api/routes/health.py`, update the Redis client construction in
   `health_check()` to use `settings.redis_url`.
3. Preserve the existing health response structure, Redis check behavior, and
   error logging.

This plan does not add a second configuration setting, change the Redis
service, alter the PostgreSQL or vector-database checks, upgrade dependencies,
or broaden the health endpoint. The separate PostgreSQL/SQLAlchemy failure
observed during reproduction remains out of scope.

## Plan comment

I plan to fix issue #62 by correcting the Redis health probe's configuration
lookup. Redis is reachable (`redis-cli ping` returns `PONG`), but
`health_check()` reads `settings.redis_host`; `Settings` defines `redis_url`
instead, so the probe raises `AttributeError` and `/health` reports Redis as
unhealthy.

I will make the smallest fix in `api/routes/health.py` by using the existing
`settings.redis_url` field when creating the Redis client. I will preserve the
current response and logging behavior and will not change the Redis service,
the PostgreSQL or vector-database checks, dependencies, or unrelated health
endpoint behavior. This investigation and plan were AI-assisted with Claude
Code; I will verify the implementation and test results myself.

## Test plan

### Reproduction-level verification

1. Start the backing services:

   ```text
   docker compose up -d db redis
   ```

2. Confirm Redis is reachable:

   ```text
   docker exec pathreview-ai301-fa26-s1-redis-1 redis-cli ping
   ```

   The output must be `PONG`.

3. Start the API:

   ```text
   uvicorn api.main:app --host 127.0.0.1 --port 8000
   ```

4. Call the health endpoint:

   ```text
   curl -s -i http://127.0.0.1:8000/health
   ```

   The response must report `"redis":"healthy"` under `dependencies`, and the
   application log must no longer contain
   `Settings' object has no attribute 'redis_host'`. The overall response may
   remain HTTP 503 if the separate PostgreSQL check remains unhealthy.

### Automated verification

Add or run a focused health-check test that supplies a `redis_url` and verifies
that the Redis probe creates or uses the client with that URL and successfully
reports Redis healthy. The test must fail before the change because the code
reads `redis_host`, and pass after the change.
