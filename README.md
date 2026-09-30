# Library Management System

Node.js + Express backend, HTML/CSS/JS frontend.
- **SQL (MySQL):** users, sections, books, borrowals (`schema.sql`)
- **NoSQL (MongoDB):** activity log

## Run
1. Install Node 18+, MySQL and MongoDB, and start both.
2. `npm install`
3. `cp .env.example .env` and set your MySQL password.
4. `npm start`, then open http://localhost:3000

Registration: students sign up freely at `/register.html`. Admin (librarian) sign-up needs the `ADMIN_CODE` from `.env` (default `LIBRARY-ADMIN`, change it).

Default librarian: `librarian@library.com` / `admin123` (change it). The librarian adds students from the dashboard.

## Demo time machine
With `DEMO_MODE=true` the student page shows Skip 7 days / Skip 20 days / Reset buttons. Skip ahead, then return a book to see a fine (late) or reward points (on time). It shifts the date for all users; set `DEMO_MODE=false` for real use.

## Payments
Students pay fines from the student page (UPI, card or net banking) and get a receipt number. The librarian can also mark a fine paid in cash and sees all payments. Students can't borrow while a fine is unpaid.
Payments here are **simulated**: no money moves. To take real payments, connect a gateway such as Razorpay or Stripe inside `POST /api/pay` in `server.js`.

## Rules (edit at top of `server.js`)
14-day loan, max 3 books, return on time = +10 points, late = 5 per day fine.
