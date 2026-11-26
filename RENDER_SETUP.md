# Dyno Core — Render deployment starter

## Important
This is a legacy Dyno Core codebase (v3.2.0), not a modern, maintained bot template.
This ZIP adds deployment notes and removes a Git-over-SSH dependency and embedded webhook URLs.
It does **not** modernize the old Discord library/API integration. Build or runtime failures are possible.

## Render setup
1. Push this folder's contents to a private GitHub repository.
2. In Render, create a **Background Worker** from that repository.
3. Runtime: Node. Build command: `npm install --no-audit --no-fund`
4. Start command: `npm start`
5. Set the environment variables listed in `.env.example`.
6. Create a Redis/Key Value service in the same region. Use its **internal** host, port and password for
   `CLIENT_REDIS_HOST`, `CLIENT_REDIS_PORT`, and `CLIENT_REDIS_AUTH`.
7. Deploy and inspect the worker logs.

## Required environment variables
- `CLIENT_TOKEN`: Discord bot token
- `CLIENT_ID`: Discord application/client ID
- `ADMIN_ID`: your Discord user ID
- `CLIENT_REDIS_HOST`, `CLIENT_REDIS_PORT`, `CLIENT_REDIS_AUTH`: Redis connection settings

Do not put secrets in GitHub. Add them only in Render's Environment settings.
Do not share your bot token or Redis password.

## Notes
- `npm start` runs `node src/index.js`.
- The separate dashboard/web process is `npm run web`; this starter does not deploy it.
- The old dependencies may fail on Render's current build environment. If installation fails, do not
  randomly upgrade packages: that can break this legacy application.
- The original source contained hard-coded Discord webhook URLs. They were removed from this ZIP.
  If the original ZIP was shared publicly, revoke/rotate those webhook URLs.
- Only run code you trust. Review the commands, modules and permissions before inviting the bot.
