Attendance Tracking
- Views: Daily and weekly attendance views.
- APIs:
  - `GET /attendance/daily?userId=` — daily records
  - `GET /attendance/weekly?userId=&weekStart=` — weekly summary

Payroll / Salary Management
3.6.1 Employee Payroll View
- Payroll data is read-only for employees: `GET /payroll/me`

3.6.2 Admin Payroll Control
- Admin can:
  - `GET /payroll` — view payroll of all employees
  - `PUT /payroll/:userId/structure` — update salary structure
  - `POST /payroll/reconcile` — ensure payroll accuracy (run checks)

Workflows
- Employee (attendance / payroll):
  1. Login → Dashboard
  2. View daily/weekly attendance (charts)
  3. View payroll (read-only)

- Admin (attendance / payroll / leave):
  1. Login → Admin dashboard
  2. View aggregated attendance and leave across employees
  3. Compare employees, adjust salary structures
  4. Reconcile payroll and publish

Charts
- Employee charts: weekly comparison (this week vs last week), daily trends
- Admin charts: comparative charts across employees — attendance rate, leave taken, salary distribution

Email verification
- Flow:
  1. User registers → backend creates user with `verified=false`
  2. Backend sends verification email with a short token link: `GET /auth/verify?token=`
  3. `GET /auth/verify` validates token and sets `verified=true`
- Implementation notes: use `JWT_SECRET` or a separate verification token; send via `nodemailer`.

Notes
- Add routes in `src/routes/attendance.js`, `src/routes/payroll.js`, `src/routes/auth.js`.
- Frontend: create charts pages in `hrms-frontend` that call the above APIs.
