FALCON PREMIUM BOT V2 — RENDER DEPLOYMENT

This package adds a small Flask health-check server and reads the bot token from DISCORD_TOKEN.

GITHUB UPLOAD (phone-friendly):
1. Extract this ZIP.
2. Upload all files inside this folder to the ROOT of a new GitHub repository (not the outer folder).
3. On Render choose New + > Blueprint, connect that repository, and let Render detect render.yaml.
   Alternatively choose New > Web Service and use:
   Build command: pip install -r requirements.txt
   Start command: python main.py
4. In Render > Environment add:
   Key: DISCORD_TOKEN
   Value: your bot token copied from Discord Developer Portal > Bot.
   Save and deploy. Do not put the token in GitHub, render.yaml, screenshots, or chats.
5. In Discord Developer Portal > Bot, enable the privileged intents this code uses:
   - Server Members Intent
   - Message Content Intent
   - Presence Intent (code enables it; enable it if you want the bot to connect successfully)
   The code also enables Invite intent. Invite the bot to your server with only the permissions it needs.
6. Open the Render service URL. /health should show OK.

CODE CHANGES ALREADY MADE:
- Added Flask dummy web server on 0.0.0.0:$PORT (default 10000).
- Replaced hardcoded BOT TOKEN placeholder with os.environ["DISCORD_TOKEN"].
- Added requirements.txt.

IMPORTANT LIMITATIONS:
- Free Render web services can spin down when idle; they are not reliable always-on Discord bot hosting. A sleeping/restarting service disconnects the bot.
- Render local files are ephemeral by default. falcon_data.db can reset on restart/redeploy unless you use a paid persistent disk and change the DB path to its mount directory. Back up the database before deploying updates.
- Music playback also needs system FFmpeg and voice support; this package installs yt-dlp but does not install the FFmpeg executable. Other bot features can run without music.
- Review the bot's permissions and security before inviting it to a real server.
