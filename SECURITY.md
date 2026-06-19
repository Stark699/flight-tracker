# Security Notes

## Known issue: API keys were previously hardcoded

In the original version of `app.py`, all API keys were written directly in the source
code as string literals. This is a security bug because:

- Anyone who can read the source code (e.g. a public GitHub repo, a leaked file, a
  screenshot) gains access to your API keys.
- Keys committed to git history remain there even after the line is deleted; they must
  be rotated at the provider dashboard.

**Fix applied:** keys are now loaded from a `.env` file via `python-dotenv`.  
`.env` is listed in `.gitignore` and is never committed.  
Use `.env.example` as a safe template.

## Login credentials

The app uses a single username/password set in `.env` (`LOGIN_USERNAME` / `LOGIN_PASSWORD`).
Change these before deploying. The password is compared in plain text — suitable only
for a personal/demo app; do not use this pattern for a production system.
