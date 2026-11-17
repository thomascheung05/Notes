# Notes

Quick-access notes site for GitHub Pages.

**Add a new tab:** create `notes/<name>.md`, then add a line to the `TABS` list near the bottom of `index.html`:

```js
{ name: "Python", file: "notes/python.md" },
```

**Preview locally:** `python -m http.server` then open http://localhost:8000
(opening `index.html` directly as a file won't load the notes — browsers block that).
