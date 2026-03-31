# Changelog

## v0.9.0

### Features

* **Gzip compression** — all requests send `Accept-Encoding: gzip`, responses are decompressed transparently. ~19x reduction in response payload size.
* **Batch delete** — `HintDeleteFilter.ID` changed from `int` to `[]int`, supporting batch delete of up to 1000 rules per API call.
* **IP list cache support** — `IPListReadByRuleType` method for per-rule-type filtered reads, `IPListSearch` for targeted value lookup.
* **Hits fetch by attack_id** — fetch related hits across an attack campaign for false positive analysis.
* **Credential stuffing configs** — `CredentialStuffingConfigsRead` method for the v4 API endpoint.
* **Action API methods** — `ActionReadByHitID` for resolving hit-to-action mapping.

### Improvements

* **HTTP header handling** — request headers are now copied (not replaced), preserving Go's default transport headers.
* **APIError type** — structured error with `StatusCode` and `Body` fields, compatible with `errors.As()`.
* **Retry policy** — configurable retry for 423 (rules locked), 5xx (server error), and 429 (rate limit) with exponential backoff.
* **Pagination fix** — all paginated methods set `response.Body.Objects = nil` before each `json.Unmarshal` to prevent slice reuse bugs.

### Documentation

* **README rewrite** — updated capabilities list, added features section (retry, gzip, structured errors), updated code examples.

### Breaking Changes

* `HintDeleteFilter.ID` type changed from `int` to `[]int` — callers must wrap single IDs in `[]int{id}`.
* `ClientFields.Enabled` changed from `bool` to `*bool` (fixes `omitempty` dropping `false`).
