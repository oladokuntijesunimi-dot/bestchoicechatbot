# Molete (Ibadan) Best Choice Multipurpose Co-operative Society — AI Assistant

Flask app with a member-facing chatbot and an admin portal for managing the
knowledge base. No vector database, no chunking — every chat request sends
the full contents of `information.txt` to Groq alongside the member's
question, and Groq is prompted to synthesize a fresh, natural answer.

## Setup

```bash
pip install -r requirements.txt
cp .env.example .env
# edit .env: set GROQ_API_KEY, FLASK_SECRET_KEY, and admin credentials
python app.py
```

Then open:
- Member chatbot: http://localhost:5000/
- Admin portal: http://localhost:5000/admin (redirects to login)

## Notes

- `GROQ_MODEL` defaults to `llama-3.3-70b-versatile` — change it in `.env`
  if you'd like a different Groq-hosted model.
- Admin password changes made from the dashboard live in memory only and
  reset to the `.env` value on server restart. Update `.env` directly if
  you want a change to persist across restarts.
- `information.txt` is read fresh from disk on every chat request, so
  edits made in the admin portal take effect immediately with no restart
  or re-indexing required.
- For production, run behind gunicorn/uwsgi + a reverse proxy, set
  `debug=False`, and use a strong, random `FLASK_SECRET_KEY`.
