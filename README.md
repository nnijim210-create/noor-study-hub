# NOOR — Medical Study Hub

A static medical resource library. No backend or paid APIs required.

## Preview locally

Run `python -m http.server 8000` from this folder, then open http://localhost:8000. Opening `index.html` as a file directly may block loading JSON.

## Publish on GitHub Pages

1. Create a new **public** GitHub repository, e.g. `noor-medical-hub`.
2. Upload **the contents** of this folder to the repository root, preserving paths.
3. Go to **Settings → Pages → Build and deployment**. Choose **Deploy from a branch**, branch **main**, folder **/(root)**, then Save.
4. Wait for deployment and open the URL GitHub provides, typically `https://USERNAME.github.io/noor-medical-hub/`.
5. To update the library, commit changes to `data/library.json` and upload resource files under `resources/`. GitHub Pages redeploys after commits.

GitHub Pages sites are public; do not publish copyrighted/private materials without permission. GitHub Pages has published limits (including repository/site size and bandwidth guidance); review the latest GitHub Pages usage limits before large uploads.

## Resource registry

Edit `data/library.json`. Each subject has an `id`, `title`, and a `chapters` array. Example chapter:

```json
{"id":"ch1","number":1,"title":"Introduction","description":"Overview","requirements":"Pages 1–10","required":false}
```

Example resource in top-level `resources` array:

```json
{"id":"anatomy-exam-1","title":"Anatomy Chapter 1 Practice","type":"exam","subjectId":"anatomy","chapterId":"ch1","path":"resources/anatomy/ch1/exam/index.html","description":"Original HTML exam","questionCount":null,"instructions":""}
```

Use unique IDs. Supported types: `exam`, `flashcards`, `summary`, `pdf`, `image`, `html`, `document`, `other`. For native flashcards, omit `path` and add `cards: [{"front":"...","back":"..."}]`. Original HTML flashcards should use a path instead; the original remains intact.

Example optional exam preparation record in the top-level `exams` array:

```json
{"id":"midterm-a","title":"Midterm","date":null,"requiredChapters":[{"subjectId":"anatomy","chapterId":"ch1"}]}
```

## Existing HTML exams

Copy the entire original exam folder (HTML, CSS, JS, images) into `resources/<subject>/<chapter>/<exam>/`. Set `path` to its HTML entry point. The in-site preview uses a sandboxed iframe with scripts and forms, but no same-origin permission. Some existing exams require same-origin storage, popups, or unrestricted browser APIs and may fail in the iframe. Use **Open separately** in that case. Inspect untrusted HTML before publishing: separate-page opening is not a security sandbox and same-origin code may access your site's browser storage. Do not publish untrusted or sensitive files. Do not alter original exam content without permission.

## Limits

- Progress and flashcard review ratings use browser localStorage only, not cross-device sync.
- No browser-based permanent upload, authentication, accounts, or backend.
- Search indexes metadata, not full PDF text.
- Flashcard ratings are saved but do **not** implement spaced repetition.
- Missing files show a browser/network error; the registry itself does not verify file existence.
- No actual exams or PDF files are included until they are assigned and added.


## Personal first-year edition (v3)
This version is for one first-year medical student only. The sister profile selector was removed. Chapter checkboxes are initially unchecked. The chapter count for each subject is editable and can be changed without editing code. Progress is saved in the browser's localStorage only; it does not sync across devices. Existing progress stored under the `me` profile in NOOR v2 remains readable when using the same browser and site origin. If you open the site at a different address or folder path, browser storage may be separate.


## NOOR v4 — Personal study hub
- 75 chapter placeholders across 6 core subjects (plus Other), and total lecture counts (148). Lecture-to-chapter mapping intentionally left unspecified.
- Bundled original HTML quizzes, flashcards, study guide, and two small PDF study sheets in `resources/`. No content of original files was edited.
- Add resources: select subject, chapter, section and file; files are stored in IndexedDB in that browser, metadata in localStorage. They are **not** automatically included in ZIP or synced across devices.
- Study Planner: add dated tasks and mark them done; tasks and chapter progress are local browser data.
- Open via a local web server (e.g. `python -m http.server 8000` in the NOOR-v4 folder) or GitHub Pages. Direct `file://` opening may block the JSON manifest.
- The Midterm and Final dates are ranges only; exact subject exam dates were not provided.
