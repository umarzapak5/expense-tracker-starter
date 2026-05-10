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

React + Vite app with no routing, no context, and no external state library. Components live under `src/components/<ComponentName>/<ComponentName>.jsx`.

**State ownership:**
- `App` — owns `transactions` array and `categories`. Passes data down; does not compute derived values itself.
- `Summary` — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- `TransactionForm` — owns its own form state (`description`, `amount`, `type`, `category`). Calls `onAdd(transaction)` prop on submit.
- `TransactionList` — owns filter state (`filterType`, `filterCategory`). Receives `transactions` and `categories`, filters internally for display.

**Data flow:** `App` passes `transactions` to `Summary` and `TransactionList`, and an `onAdd` callback to `TransactionForm`. Nothing is persisted — state resets on page reload.

**Transaction shape:** `{ id, description, amount, type, category, date }`. `amount` is a number. `type` is `"income"` or `"expense"`.

**Categories** are a hardcoded array in `App`: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`. Any new category must be added there.

**Styling:** Flat CSS in `src/App.css` with class names like `.income-amount`, `.expense-amount`, `.balance-amount`. The `.delete-btn` class exists in the CSS but the delete button is not yet rendered in the JSX.
