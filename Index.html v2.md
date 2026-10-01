Ok# UniOS backend setup

This version adds:

- Email/password sign-up and login
- Persistent student sessions
- A private cloud workspace per user
- Cloud saving/loading of deadlines, notes and grades
- JSON import/export
- The existing UniOS dashboard and focus/calendar/grade features

## 1. Create a Supabase project

Create a free Supabase project at https://supabase.com/.

## 2. Create the database

In Supabase, open **SQL Editor** and run the contents of `supabase-schema.sql`.

The SQL creates `public.user_workspaces`, enables Row Level Security, and limits each signed-in user to their own workspace.

## 3. Get your Supabase credentials

In Supabase, open your project's API settings and copy:

- Project URL
- Publishable key

Do **not** put a `service_role`/secret key into the website. The browser version is intended to use the publishable key with Row Level Security enabled.

## 4. Configure the website

Open `index.html` and find:

```js
const SUPABASE_URL='PASTE_YOUR_SUPABASE_URL_HERE';
const SUPABASE_PUBLISHABLE_KEY='PASTE_YOUR_SUPABASE_PUBLISHABLE_KEY_HERE';
```

Replace those two values with your project's URL and publishable key.

## 5. Upload to GitHub

Replace your current GitHub Pages `index.html` with this version and commit the change.

Your live UniOS site will then show the login screen. A student can create an account and their dashboard data will be saved to their own cloud workspace.

## 6. Email confirmation

Supabase Auth may require users to confirm their email before the first login. In the Supabase Auth settings, configure the site URL and redirect URL to your live GitHub Pages URL.

## Current MVP architecture

GitHub Pages hosts the frontend.

Supabase Auth handles accounts/sessions.

Supabase Postgres stores one private JSON workspace per user.

The next commercial iteration should move tasks/notes/grades into separate database tables once usage patterns are validated. That will make reporting, sharing and more advanced features easier to build.
