# Targeted API corrections

This project includes source-level fixes for the song suggestion and lyrics routes:

- `/api/songs/{id}/suggestions`: validate and cap `limit` to 1–50, send the normalized limit upstream, avoid caching transient station/suggestion responses, avoid pre-encoding the song ID before JSON serialization, and return an upstream `502` instead of a generic `500` when JioSaavn is unavailable.
- `/api/songs/{id}/lyrics`: recognize common truthy upstream lyrics flags and attempt lookup using `lyricsId` first, then the song ID if the first lookup returns no lyrics. Return a clear `404` only when no lyrics can be retrieved.
- Suggestion payload parsing skips malformed upstream items rather than failing the entire response.

A successful build and live endpoint test could not be run in this environment because dependencies could not be installed (the `next` executable was unavailable). Deploy and test the endpoints after installing dependencies in CI/Vercel.
