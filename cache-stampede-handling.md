# Handling Cache Stampede in Production

## Problem

A cache stampede happens when:

- Cached data expires
- Multiple requests hit the backend simultaneously
- Database or downstream service gets overloaded
- System latency spikes or crashes

This usually happens under high traffic.

---

## Example Scenario

- Popular API endpoint
- Cache TTL = 5 minutes
- Cache expires
- 5,000 concurrent users hit the same endpoint
- All requests bypass cache
- Database load explodes

Result:
High latency or outage.

---

## Solutions

### 1. Cache Locking (Mutex)

Allow only one request to rebuild cache.
Other requests wait or serve stale data.

---

### 2. Stale-While-Revalidate

Serve stale cache temporarily.
Refresh cache in background.

Improves user experience under load.

---

### 3. Randomized Expiry (Jitter)

Instead of fixed TTL:
TTL = base + random offset

Prevents simultaneous expiration.

---

### 4. Rate Limiting

Protect backend during spike.
Return controlled responses instead of crashing.

---

## Key Lesson

Design for failure.
Assume traffic spikes.
Assume cache will expire at worst time.

Production engineering is about prevention,
not reaction.

— CodeWithIshwar
