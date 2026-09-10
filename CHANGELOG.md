## Release Notes

## [1.1.0]

### Fixed

- `Webhook.Execute()` built an invalid query string (`&?wait=true`) when a `threadID` was
  passed, so Discord never returned the created message body and `Webhook.Edit()` could not
  be used afterwards.
- `Embed.GetField()` / `Webhook.GetEmbed()` used an inverted bounds check
  (`array.Length < index`), returning `null` for every valid index and reading out of bounds
  for invalid ones.
- Memory leaks: the `JSONArray` handles obtained in `AddField()`, `AddEmbed()`, `GetField()`
  and `GetEmbed()` were never freed.
- Sub-object / array getters (`GetFooter`, `GetImage`, `GetThumbnail`, `GetVideo`,
  `GetProvider`, `GetAuthor`, `GetFields`, `GetEmbeds`) raised a native error instead of
  returning `null` when the key was not set.
- `Embed.SetTimeStampNow()` used a malformed format string (`"%FT\%T.000%z"`).
- `DEBUG` build path did not compile (`this.toString` instead of `this.ToString`) and passed
  unescaped JSON as a format string to `PrintToServer`.
- URL buffers in `Execute()` / `Edit()` could truncate a near-maximum-length webhook URL.

### Added

- `Webhook.GetThreadName()`.
- `Webhook.Execute()` now skips the `thread_id` query parameter when `thread_name` is set,
  avoiding Discord error `220002` (a forum webhook cannot use both).

### Changed

- `Webhook.SetThreadName()` now takes a `const char[]` and its documentation reflects the
  real Discord limit of 100 characters.

## [1.0.0]

### Added

- Initial release.
