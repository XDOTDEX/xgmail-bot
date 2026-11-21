# 🤖 Gmail Bot

**Your Gmail in Telegram — with multiple accounts.** The official Gmail bot allows only one Gmail account; this one lets every user connect many, get every new mail (inbox **and** spam) inside Telegram, and reply without leaving the chat.

Made by [DEメTER](https://t.me/xdotdexter) · Channel: [@btcmoonx](https://t.me/btcmoonx)

## What it does

- 📥 **New mail in Telegram** — inbox and spam, checked every minute, with the receiving account shown on every mail.
- 🔑 **Code highlight** — verification codes are pulled out of the mail and shown in a tap-to-copy block.
- 👁 **Show more / Less** — long mails expand in place.
- ⚙️ **Actions on every mail** — ✉️ Reply (threaded), Forward (draft flow with recipient + extra message), mark read/unread, archive / back to inbox, trash, spam, **Hide emails from sender**, **🚫 Unsubscribe** (one-click where the mail supports it), **Hide all 'category' emails**.
- 📎 **Attachments** — listed on the mail and downloadable.
- 👥 **Multiple Gmail accounts per user** — the headline feature.
- 👁 **Track friends** — get a message when a tracked Telegram user comes online.
- 🔒 **Members only** — the bot works only for @btcmoonx channel members, on **every** plan; paid users get no exemption. Leaving pauses the service; all data is kept.
- 🧹 **History stays** — the bot never deletes chat history.
- 🗄 **Automatic backup** — the owner receives a full backup zip every day (and with `/backup`); restore on a new phone from the zip alone (see RESTORE.txt inside it).
- 🔁 **Boot auto-start** — with Termux:Boot, bot + watcher start when the phone turns on.

## Plans

| | Free | Premium 1 | Premium 2 |
|---|---|---|---|
| Gmail accounts | 3 | 20 | Unlimited |
| Tracked friends | 3 | 20 | 20 |
| Price (Telegram Stars) | — | 100 ⭐ / 2 months | 500 ⭐ / 6 months |

When a premium ends, the free plan runs automatically and only the **first** Gmail account keeps receiving mail. **Telegram Premium users get a free boost: 4 Gmail accounts and 5 tracked friends.** The weekly Fuckgames Top 3 can claim **Premium 1 free** (first 3 claims each month) with `/freeallservice`. The owner has everything unlimited.

## Commands

| Command | What it does |
|---|---|
| `/start` | Start + menu |
| `/father` | About the creator |
| `/accounts` | Your connected Gmail accounts |
| `/add` | Connect a Gmail account (Google sign-in) |
| `/remove <n>` | Disconnect an account |
| `/latest` | Show the latest mails now |
| `/premium` | Plans + buy with Stars |
| `/freeallservice` | Top 3 players claim free Premium 1 |
| `/track <user>` · `/untrack <user>` · `/tracking` | Online tracking |
| `/status` | Your plan and usage |
| `/backup` | Owner only: send a full backup zip |
| `/cancel` | Cancel the current action |

## Setup (Termux, ~15 minutes)

1. **Create the bot** in @BotFather (`/newbot`) and keep the token.
2. **Google Cloud** (console.cloud.google.com):
   - Create a project → enable the **Gmail API**.
   - OAuth consent screen: External; add the Gmail users as **test users**.
   - Credentials → Create OAuth client ID → type **Desktop app**. Keep the **client_id** and **client_secret**.
3. **Install**:
   ```
   pkg install python -y
   pip install requests telethon
   unzip <zip> -d ~/gmail-bot && cd ~/gmail-bot
   python3 setup.py        # 5 values, typed at the prompts only
   ```
4. **Run**:
   ```
   nohup python3 gmail_bot.py > gmail.log 2>&1 &
   python3 gmail_watch.py  # first run: phone + code login
   ```
5. **Boot auto-start** (optional): install the **Termux:Boot** app (same store as your Termux), open it once, then:
   ```
   mkdir -p ~/.termux/boot && cp start-gmail-bot.sh ~/.termux/boot/ && chmod +x ~/.termux/boot/start-gmail-bot.sh
   ```

Users connect Gmail with `/add`: the bot gives a Google sign-in link; after Allow, the browser lands on a dead `localhost` page — the user copies the full address-bar link back to the bot, and the account is connected. No password ever touches the bot.

## Files

- `gmail_bot.py` — the bot (Telegram + Gmail + plans + backups)
- `gmail_watch.py` — Telethon online-status watcher (own session)
- `setup.py` — one-time secret entry (values stay on the phone)
- `start-gmail-bot.sh` — Termux:Boot auto-start
- Secrets (`config.json`, `tg_config.json`, `google_config.json`) and user data are **never** committed to GitHub.

## Updates

- **Refer & Earn:** every user gets a personal referral link (/referral). A new user joining through it earns the referrer **100 $XOX** (tracked in the bot, shown in /status).
- **Maintenance mode (owner):** /maintenance on|off - while on, every non-owner user gets the maintenance reply.

- **Referral verification:** referral credit is no longer instant. A referral stays pending ~48 hours and is credited only if the referred user is still a channel member AND has really used the bot (fake/VPN farm accounts that only tap /start never pass). Leaving the channel cancels it; never using the bot expires it after 14 days. Max 10 verified credits per referrer per day.

## Latest update

Referrals are **instant** again: **5 $XOX per referral**. Bursts of referrals trigger warning messages instead of blocking (5+ in an hour, 10+ or 20+ in a day - warning to the referrer plus a notice to the owner); referrals still count. New: **/convert** - turn $XOX into Premium: **50 $XOX = 10 days**, **100 $XOX = 30 days**.

**Update:** referrals are now **unlimited** - no warnings, no caps. Every referral instantly earns 5 $XOX.

**Update:** new - @btcmoonx channel posts are now copied to all bot users automatically. Premium users can opt out with /posts off (Free plan always receives them). Messages sent while the bot was off get a maintenance reply.

## Update — v10

- The Play Fuckgames button and link now open the game bot @BedBouncebot (https://t.me/BedBouncebot) instead of the web page — the game must be played through the game bot so the leaderboard records the player Telegram id and the free Premium claim can match.
