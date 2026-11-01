# Pigeonhole

**Find duplicate emails, tidy messy folders and keep your mailbox lean, on your own Mac.**

Pigeonhole works with **iCloud Mail** and **Google (Gmail)** accounts, and can also look at the mail already stored on your Mac. Everything runs locally: your mail goes straight between your Mac and your mail provider, and nothing is sent to us or anyone else.

> Not affiliated with Apple or Google. Pigeonhole moves mail to Trash and can undo what it does, but it is still your mail: keep a backup of anything you can't afford to lose.

## Download

1. Go to **[Releases](https://github.com/daviddef/PigeonHole-Public-/releases/latest)** and download `Pigeonhole-x.y.z.dmg`.
2. Open the DMG and drag **Pigeonhole** into **Applications**.
3. Open Pigeonhole from Applications. It is signed and notarised by Apple, so it opens without warnings.

Needs macOS 12 (Monterey) or later, on Apple silicon or Intel. You don't need to install anything else: Python is included.

## What it does

| Tab | What you can do |
| --- | --- |
| **Connect** | Sign in to iCloud or Google (more than one account is fine), see every folder with message counts and date ranges, and spot empty folders. **Live growth** shows folder counts and sizes changing as mail arrives or moves. |
| **Scan** | Reads message headers to find duplicates (same Message-ID), including copies in different folders. Shows live progress, speed and time left. Nothing is changed. |
| **Review** | See every duplicate group, choose which copy to keep (by folder, or "prefer filed folders"), then move the extras to Trash. |
| **Tidy up** | **Merge folders**: combine look-alike folders such as "Sent Items" and "Sent Messages". **Archive by year**: move old mail out of a busy folder into year folders. **Large messages**: find the biggest messages, filter by size and age, save or strip attachments to disk. **Empty folders**: remove folders with no mail. |
| **Local mail** | Look through mail stored on this Mac (read-only) to find large messages and attachments. |
| **History** | Every change is recorded. Undo most of them with one click. |

## First launch

1. Open Pigeonhole. A window appears with the **Connect** tab.
2. Choose **iCloud Mail** or **Google (Gmail)**, type your address and an **app-specific password** (not your normal password). See [How to get an app password](docs/app-passwords.md).
3. Tick **Remember in the macOS Keychain** if you want it to remember the account. The password is stored only in your Mac's Keychain.
4. Pick the folders to scan and press **Start scan**.

## Local mail (optional)

To read mail stored on your Mac, macOS asks you to allow it:

1. Open **System Settings > Privacy & Security > Full Disk Access**.
2. Switch **Pigeonhole** on (press **+** to add it if it isn't listed).
3. Quit Pigeonhole and open it again.

Pigeonhole only reads Mail's files and never changes them.

## Is it safe?

- **Duplicates are moved to Trash, not deleted.** You can restore them from History or from the Trash folder itself.
- **Nothing happens until you confirm.** Scans only read headers.
- **Each move is checked against the server first**, so a message that changed since the scan is left alone.
- **Stop buttons** on every task. Quitting mid-task asks you first; what already moved is kept in History.
- **No cloud, no account, no tracking.** Pigeonhole talks only to your mail provider. See [Privacy](#privacy).

## Privacy

- Your mail and passwords never leave your Mac, except to your own mail provider (iCloud: `imap.mail.me.com`, Google: `imap.gmail.com`).
- Passwords are kept in the macOS Keychain, only if you tick "Remember".
- Settings, history and recent accounts are kept in `~/.icloud_dedupe` (open it from **Help > Open Pigeonhole's data folder**).
- Attachments you choose to save are written to `Documents/Pigeonhole`.
- No analytics, no crash reporting, no updates check.

## Troubleshooting

See [docs/troubleshooting.md](docs/troubleshooting.md). Common ones: login failed (use an app password), "macOS is blocking access to Mail's folder" (grant Full Disk Access), iCloud rejecting large uploads (use **Large messages**).

## Uninstall

Quit Pigeonhole and drag it from Applications to the Bin. To also remove its data, delete `~/.icloud_dedupe`, and the Pigeonhole items in Keychain Access if you ticked "Remember".

## Licence

Free to use for personal use, provided as is without warranty. Copyright David Defranceski. See [LICENSE](LICENSE).
