# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

No test suite is configured.

## Architecture

This is a single-file React app (`src/App.jsx`) — all state, logic, and UI live in one `App` component. There is no routing, no context, no custom hooks, and no external state library.

**State:** `transactions` is the core array; each item has `{ id, description, amount, type, category, date }`. `amount` is stored as a string (not a number) — this is a known bug that causes incorrect totals via string concatenation instead of numeric addition.

**Data flow:** All derived values (totals, filtered list) are computed inline during render from the `transactions` array. Nothing is persisted — state resets on page reload.

**Categories** are a hardcoded array: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`. Any new category must be added there.

**Styling:** Flat CSS in `src/App.css` with class names like `.income-amount`, `.expense-amount`, `.balance-amount`. The `.delete-btn` class exists in the CSS but the delete button is not yet rendered in the JSX.
