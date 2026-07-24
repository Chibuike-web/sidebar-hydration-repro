# Sidebar hydration reproduction

Standalone Next.js preview app for the async sidebar state issue.

## Run

```powershell
bun run dev
```

Then open `http://localhost:3000`.

## Verify

1. Run `localStorage.setItem("sidebarState", "collapsed")` in DevTools and reload.
2. Inspect `<html>` immediately: the head script sets `data-sidebar-state="collapsed"` before hydration.
3. The sidebar waits 1.2 seconds, but `Suspense fallback={null}` does not change the root layout state.
4. Toggle the sidebar after it resolves and confirm the root attribute and localStorage update together.
5. Use the secondary route to observe a real Next `<Link>` prefetch target.

`next.config.ts` enables `cacheComponents` and top-level `partialPrefetching` for this preview release.
