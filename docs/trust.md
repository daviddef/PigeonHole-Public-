# Is Pigeonhole safe to trust with my mail?

Pigeonhole asks for an app password, so it is fair to ask what it does with it. This page says exactly what it does, and how you can check each claim yourself.

## In short

- Your mail is never uploaded anywhere. Pigeonhole has no server of its own.
- It talks only to your mail provider (`imap.mail.me.com` for iCloud, `imap.gmail.com` for Google), plus the two accounts you pick if you use **Move mail**.
- Your app password is kept in the macOS Keychain, and only if you tick "Remember". It is never written to a file or a log.
- It sends no analytics, no crash reports and no "phone home" messages.
- Removing messages moves them to Trash and can be undone from **History**. Pigeonhole never empties your Trash.

## What it connects to

| What | Where | Why |
|---|---|---|
| Your mailbox | `imap.mail.me.com:993` or `imap.gmail.com:993` (encrypted) | Reading folders and moving messages |
| The page you see | `127.0.0.1` (this Mac only) | The app window talks to a small helper running on your own Mac |

Nothing else. **You can check this yourself:** run a network monitor such as Little Snitch, or in Terminal:

```bash
nettop -m tcp -p Pigeonhole
```

You should see only the hosts above.

## Your password

- Use an **app-specific password**, not your normal one. You can create and revoke these at any time: [how](app-passwords.md). Apple lets you keep up to 25 and revoke each one separately, so you can create one just for Pigeonhole and delete it when you are done.
- "Remember in the macOS Keychain" is off by default. If you turn it on, the password is stored in your login keychain under the account name, the same way Mail stores it.
- The password is held in memory while you are connected and is cleared when you disconnect or quit.

## What is on your disk

Everything lives in `~/.icloud_dedupe` on your Mac: your account names (not passwords), settings and the undo history. Delete that folder and Pigeonhole forgets everything. Pigeonhole never changes mail files on your Mac. "Local mail" only reads.

## How it is built and signed

- Signed with an Apple **Developer ID** and **notarised** by Apple, so macOS has checked it for known malware. Check: `spctl -a -vv /Applications/Pigeonhole.app` should say "accepted, source=Notarized Developer ID".
- It uses only Python's standard library plus its own code. There are no third-party packages to inspect or update. The bundled Python is the standalone CPython build from the python-build-standalone project (Python Software Foundation licence).
- Hardened runtime is on. The app asks for no camera, microphone, contacts or location access.
- "Full Disk Access" is optional, and only needed for the **Mail on this Mac** feature, because macOS protects Mail's own folder.

## Is it open source?

No. Pigeonhole is **free for personal use, but closed source**. The licence is in the [LICENSE](../LICENSE) file. The documentation here is public so you can read what the app does, but the source is not published, so the checks above (network monitor, notarisation, Keychain) are how you verify it rather than reading the code.

## Safety rules it follows

1. Scanning only reads. Messages are fetched with a "peek", which does not mark them as read.
2. Before moving anything it re-checks each message is still the one it found.
3. Removed messages go to Trash, never straight to deletion, and **History → Undo** puts them back.
4. After a move it re-reads the folder counts from the server and tells you whether they changed by exactly the planned amount.
5. When it is not sure two messages are the same (for example no Message-ID), it leaves them ticked "Leave alone" until you decide.
6. **Move mail** copies; it never deletes from the source unless you separately choose to, after the copy has been verified.

## Reporting a problem

Open an issue on this repository. Please do not post passwords or mail contents.
