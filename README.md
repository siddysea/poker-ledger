# Poker Ledger v1 — offline-first iPhone poker bookkeeping

A self-owned, static PWA. No account, tracking, backend, fees, or third-party JS dependencies.

## Deployment
1. Create a public GitHub repository for the code. **Never put exported backup files in this repository**: game data should remain on your phone.
2. Upload all files in this folder to the repository root, including the `sw.js` and `manifest.webmanifest` files.
3. Open **Settings → Pages** in that repository, set deployment to **Deploy from a branch**, choose `main` and `/ (root)`, and save.
4. Visit your HTTPS GitHub Pages site in **Safari** on the iPhone.
5. Safari Share → **Add to Home Screen** → Add; open the installed Poker Ledger icon once while online.
6. Confirm that the app loads with Airplane Mode enabled before relying on it at a game.

## Data safety
- Every mutation is written to IndexedDB before the screen is rerendered. Transactions are append-only where possible; voiding leaves an audit record.
- Local browser storage is not a guaranteed backup. Use **Settings → Export full backup** after every poker session, and save the downloaded JSON to Files/iCloud Drive. Export before major edits. iOS may delete website data or storage; reinstalling or changing device does not sync records.
- Importing a backup **replaces** all current local data, with confirmation.
- Full session histories remain editable by reopening a closed game.
- A cash mismatch can be closed with an attribution note but will still be labeled **unresolved** in the cash ledger. The app does not pretend a player covering a shortage creates missing cash; record actual money movement accurately before certifying a settlement.
- Payment routing may be customized, but the app verifies that the transfer list correctly fulfills each player's exact net balance before marking payments as paid.
- To reverse an actual payment, edit the settlement and re-record correct paid state after independently confirming the real-world payment.

## Limitations / next iteration
- One device only, no automatic synchronization. Export backups yourself.
- Initial transactions support full-entry voiding, not replacing or altering an original record in place. Record corrected entry afterward.
- Settlement exact minimization supports up to 12 nonzero balances; above that it uses a valid greedy fallback and reports that it is not proven optimal.
- Manual discrepancy resolution records disposition and explanation, but does not yet support structured per-player attributed dollar allocations, nor does it make unbalanced cash totals automatically settleable.
- Timestamps are local-device timestamps, and payment 'paid' flags reflect operator input, not verification from Venmo or a bank.
- The application has not been professionally security-audited. Cross-check amounts before transmitting money.

## Developer checks
Run `node tests.mjs` with Node.js 18+ to test cents parsing, ledgers, and settlement invariants. No npm install needed.
