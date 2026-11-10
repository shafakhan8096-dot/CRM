# TeamDesk — Digital Marketing Team Manager

A bilingual (English/Bangla), shared online workspace for a digital marketing team. Built with React + Vite and Supabase (Auth + PostgreSQL + Row Level Security).

## Included in this MVP

- Email/password login through Supabase Auth
- Shared dashboard with task totals, completed, in-progress and overdue counts
- Task creation, assignment, due dates, priorities, status updates and CSV export
- Daily work reports with notes, hours, optional task association and evidence URL
- Team directory with roles: Admin, Team Leader, Designer, Digital Marketer
- Recurring responsibility list (daily / weekly / monthly)
- Team performance summary
- English and Bangla interface toggle
- Responsive layout for desktop, tablet and mobile

## 1. Create the cloud database

1. Create a project at [Supabase](https://supabase.com/).
2. Open **SQL Editor** in the Supabase dashboard.
3. Paste and run `supabase/schema.sql`.
4. In **Project Settings → API**, copy the Project URL and `anon` public key.

## 2. Create the first admin account

1. In Supabase, open **Authentication → Users → Add user**.
2. Create an account with the admin email and a secure password.
3. Copy the user's UUID.
4. In the Supabase SQL Editor, run the following after replacing the values:

```sql
insert into public.profiles (id, full_name, email, role)
values ('AUTH-USER-UUID', 'Workspace Admin', 'admin@example.com', 'admin');
```

Use the exact UUID and email from the Auth user you created. Do not expose the password or service-role key.

## 3. Run locally

Install Node.js 20 or newer, then:

```bash
npm install
cp .env.example .env
```

Edit `.env`:

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
```

Then run:

```bash
npm run dev
```

Open the local URL shown by Vite (usually `http://localhost:5173`).

## 4. Add team members

For each designer or marketer:

1. Create their account in Supabase **Authentication → Users → Add user**.
2. Copy the generated UUID.
3. In TeamDesk, sign in as Admin and open **Team members → Add member**.
4. Enter their UUID, full name, email and role.

Team members can then log in with their own email and password. They can view shared tasks and submit their own daily reports. Admins and Team Leaders can create and manage tasks, routines and profiles.

## 5. Deploy and publish on GitHub

1. Create a new empty GitHub repository.
2. Upload this project (do not upload `.env`).
3. For a public deployment, import the repository into [Vercel](https://vercel.com/) or [Netlify](https://www.netlify.com/).
4. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` as deployment environment variables.
5. Set the build command to `npm run build` and output directory to `dist`.

The Supabase anon key is designed for browser use when Row Level Security policies are enabled. **Never put a Supabase service-role key in the frontend or commit secrets to GitHub.**

## Notes / next iteration

This is a functional MVP scaffold, not a fully audited enterprise application. Before using it for sensitive company operations, test the RLS policies with separate admin and member accounts. Potential next improvements: routine completion history, file uploads via Supabase Storage, report approval, notifications, audit log, and richer date-range analytics.
