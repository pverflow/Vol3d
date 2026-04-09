# Contributing to Vol3D

Thanks for contributing.

This project is a shader-heavy, browser-first 3D volume texture generator with a Windows desktop packaging layer. Contributions are most useful when they preserve both:
- the **web workflow**
- the **desktop/Tauri workflow**

---

## Before you start

Please read:
- [`README.md`](README.md)
- [`docs/windows-release.md`](docs/windows-release.md)
- [`FutureFeatures.md`](FutureFeatures.md)

If you are changing app behavior, UI structure, shader logic, export format behavior, or packaging scripts, keep documentation in sync.

---

## Local setup

### Web app
```powershell
npm install
npm run dev
```

### Production web build
```powershell
npm run build
```

### Desktop app
```powershell
npm run tauri:dev
```

### Desktop packaging
```powershell
npm run tauri:build
```

---

## What kinds of contributions are welcome

- bug fixes
- UI polish
- shader correctness / stability improvements
- export improvements
- better documentation
- preset workflow improvements
- performance improvements that do not reduce output quality or usability
- desktop packaging / release quality improvements

---

## Coding guidelines

### General
- Keep changes **small and focused**.
- Avoid unrelated refactors in the same change.
- Prefer fixing the root cause instead of layering workarounds.
- Preserve existing naming and file organization unless a restructure is clearly justified.

### TypeScript
- Keep strict typing intact.
- Avoid adding loose `any` types unless absolutely necessary.
- Reuse existing state and type definitions instead of duplicating shape declarations.

### GLSL / rendering
- Be careful with shader changes.
- Test both compile-time and runtime behavior.
- Watch for:
  - WebGL2 compatibility
  - precision issues
  - implicit branching costs
  - preview vs export mismatches
  - tileability regressions
- If you change uniforms, trace the full path:
  - types
  - defaults
  - state normalization
  - UI controls
  - uniform upload
  - shader usage

### UI / UX
- Keep controls discoverable.
- Preserve right-click reset behavior where it already exists.
- Avoid adding controls that are only relevant in one mode unless they are clearly gated.
- If you add a new shortcut or workflow, update the help UI and repository docs.

### Desktop support
- Browser behavior must remain functional.
- Desktop-specific improvements should degrade gracefully in the web build.
- If you add desktop file access or packaging behavior, preserve browser fallbacks.

---

## Testing expectations

Before opening a contribution, test as much as is practical.

### Minimum expected checks
```powershell
npm run build
```

If your change affects desktop packaging or native file workflows, also test:
```powershell
npm run tauri:build
```

If your change affects Windows signing/release scripts, validate the relevant release command as well.

### Manual checks worth doing
- open the app and verify the main UI loads
- verify affected shaders still compile
- verify the volume preview renders
- verify slice/projection modes still work if touched
- verify export still works if touched
- verify preset import/export still works if touched
- verify browser and desktop behavior if you changed file access

---

## Pull request guidance

A good contribution should include:
- a short summary of the problem
- a short summary of the solution
- affected files / systems
- testing performed
- screenshots or short clips for visible UI changes if available

Try to keep one PR focused on one main topic.

---

## Documentation updates

Please update docs when relevant:
- `README.md` for user-facing behavior and setup
- `docs/windows-release.md` for packaging/signing workflow
- `FutureFeatures.md` for deferred or follow-up work

---

## License note

Please review [`LICENSE`](LICENSE) before contributing. Unless explicitly agreed otherwise in writing, contributions are made under the repository’s current MIT licensing terms.


