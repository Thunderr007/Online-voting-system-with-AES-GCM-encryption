# Online Voting System (VoteVault)

A browser-based voting demo built as a **DBMS project**. One HTML file covers voter registration, OTP verification, login, voting, an in-browser database view, admin tools, and a documented SQL schema. Votes and admin exports use **AES-GCM** encryption in the browser (Web Crypto API).

## First-time setup checklist

1. Clone or download this repository (no install required).
2. Open `dbms-voting-system-v7.html` in a modern browser (Chrome / Edge recommended).
3. Register an **admin** account first (role = Admin), complete the OTP step, then log in.
4. In **Admin**, add candidates if you want names beyond the defaults.
5. Register one or more **voter** accounts, log in as a voter, and cast a vote.
6. Optional: use **DB View** to inspect the in-browser tables, and **SQL schema** for the relational design notes.

No Python, Node, or database server is required for the demo.

## Quick start

**Windows (PowerShell):**

```powershell
Start-Process "dbms-voting-system-v7.html"
```

Or double-click `dbms-voting-system-v7.html`.

Use `file://` or a local static server. WebOTP auto-fill only works in secure contexts (HTTPS or localhost) when SMS OTP is available.

## Features

- **Register / Login** — name, phone, 8-digit voter ID; roles: voter or admin
- **OTP flow** — demo OTP verification; WebOTP API support when the browser/SMS environment allows it
- **Voting** — one vote per verified voter; candidate list managed by admin
- **AES-GCM encryption** — vote payloads and admin export blobs
- **Persistence** — users, candidates, votes, and session restored from `localStorage` on the same browser/device
- **DB View** — live table snapshot of stored data
- **Admin** — add candidates, encrypted export / verify / decrypt
- **SQL schema panel** — reference schema (users, otp_requests, candidates, votes, exports) for a real DBMS backend
- **Light / dark theme** toggle

## How it works

```
Browser (single HTML + JS)
  → in-memory app state
  → localStorage (same device / same browser)
  → Web Crypto AES-GCM for vote & export payloads
```

This is a **frontend demo** of voting + DBMS concepts. For a production system you would move persistence to MySQL/PostgreSQL behind a backend API and replace the demo OTP with a real SMS provider.

## Project files

```
.
├── dbms-voting-system-v7.html   # Full app (UI + logic + schema docs)
└── README.md
```

## Demo walkthrough

| Step | What to do |
|------|------------|
| 1 | Open the HTML file |
| 2 | Register as **Admin**, verify OTP, log in |
| 3 | Add or edit candidates under **Admin** |
| 4 | Log out; register as a **Voter**, verify, log in |
| 5 | Cast a vote on **Vote** |
| 6 | Log in as admin again → check **Results**, **DB View**, encrypted export |

Default export passphrase (demo only) is set in the app state as `VoteVault-Admin-Secret` — change this if you use the project beyond local demos.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Page looks broken / blank | Use a modern Chromium browser; avoid outdated IE |
| Data gone after reopen | Same browser + same profile; “Reset saved data” or clearing site data wipes it |
| Can’t open Admin / Setup / SQL | Those pages require a logged-in **admin** |
| WebOTP never auto-fills | Needs HTTPS (or localhost) + supported browser + real SMS; you can still type the OTP manually |
| Encrypt / decrypt fails | Stay on the same browser that created the export; use the first admin’s export passphrase |

## Notes / limitations

- Data is **not** shared across devices or browsers.
- OTP is for **demo / learning** unless you wire a real SMS backend.
- Treat this as an educational VoteVault prototype, not a production election system.

## License

Personal / educational project. Use and adapt freely for coursework unless your course requires otherwise.
