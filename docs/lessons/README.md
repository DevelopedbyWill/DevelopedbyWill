# Lessons learned — DevelopedbyWill

Project-local lessons for the agency-front public repo (README + image gallery).

## How this folder works

Lessons start here. When a lesson generalizes to another project on the
same stack, **promote** it to the shared library at
`~/Development/lessons/` and add it to that library's `INDEX.md`. See
`~/Development/lessons/README.md` for the promotion procedure.

The bar for adding a new lesson:

- A bug took more than ~30 minutes to diagnose
- The root cause wasn't in the framework's docs (or was buried)
- It's likely to recur in another project on the same stack
- Future-you would benefit from the diagnosis path, not just the fix

## Cross-cutting lessons

This repo is tiny (README + images) so the shared library covers
~everything relevant:

- `~/Development/lessons/INDEX.md` — full routing by stack
- `~/Development/lessons/security-hardening-lessons.md` — relevant for
  EXIF scrub on shipped images and `.gitignore` defense-in-depth

## DevelopedbyWill-specific lessons

(none yet — add them here as `<topic>-lessons.md`)
