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

Pigeonhole has three tabs.

| Tab | What you can do |
| --- | --- |
| **Tidy** | The home screen. Connect an account, then pick a card: **Duplicate messages** (find messages that exist twice, see *why* each pair matched, keep the copy you want), **Merge folders** (combine look-alikes such as "Sent Items" and "Sent Messages"; your real Sent folder is marked **✓ real Sent** and the leftovers **leftover**), **Archive by year**, **Large messages** (find what is using your space; save or strip attachments), **Empty folders**, and **Live growth** (watch folder counts and sizes change as mail arrives). Every screen has a "← Tidy" link back. |
| **Move mail** | **Between accounts**: copy mail from one account to another (for example iCloud to Gmail) with a plan first, a check of every message afterwards, and an undo. **Mail on this Mac**: look through the mail Apple Mail keeps on this Mac (read-only). |
| **History** | Every change is recorded. Undo most of them with one click. |

### Moving mail between accounts

1. Under **Move mail → Between accounts**, connect the **From** and **To** accounts (an app password for each).
2. Press **Check what would be copied**. Nothing is changed: you get a list of folders, message counts, sizes and how long it will take.
3. Untick folders you don't want, choose a different destination folder if you like, then press **Copy**.
4. Pigeonhole copies each message with its date and read/flagged state, skips anything already at the destination (so you can run it again safely), and then checks the result against the destination.
5. Afterwards you can **Undo this copy**, or (separately, with a confirmation) **move the copied mail out of the first account into its Trash**. Pigeonhole never deletes from the first account on its own.

Good to know: iCloud accepts messages up to 20 MB and Gmail up to 25 MB. Larger ones are listed, not copied. Gmail only accepts about 500 MB of uploads a day, so a big mailbox can take several days; Pigeonhole pauses at the limit and carries on when you open it again. A message that has several Gmail labels is copied once if you leave "Copy each message once" ticked.

## First launch

1. Open Pigeonhole. A window appears with the **Tidy** tab. Press **Connect a mailbox**.
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
- **No cloud, no account, no tracking.** Pigeonhole talks only to your mail provider, unless you switch on the optional Ask Claude step in Sort Gmail (see below). See [Privacy](#privacy) and [Is Pigeonhole safe to trust?](docs/trust.md).
- **Checked afterwards.** After a move it re-reads the folders from the server and tells you whether the counts changed by exactly the planned amount.
- **Unsure matches are left alone.** Messages with no Message-ID are only matched when date, sender, subject and size all agree, and start as "Leave alone".

## Privacy

- Your mail and passwords never leave your Mac, except to your own mail provider (iCloud: `imap.mail.me.com`, Google: `imap.gmail.com`).
- Optional and off by default: **Ask Claude** (Sort Gmail) sends the sender, subject and the first ~300 characters of the messages being sorted to Anthropic's API, using your own API key. See [the trust page](docs/trust.md#optional-ask-claude-sort-gmail).
- Passwords are kept in the macOS Keychain, only if you tick "Remember".
- Settings, history and recent accounts are kept in `~/.icloud_dedupe` (open it from **Help > Open Pigeonhole's data folder**).
- Attachments you choose to save are written to `Documents/Pigeonhole`.
- No analytics, no crash reporting, no updates check.

## Troubleshooting

See [docs/troubleshooting.md](docs/troubleshooting.md). Common ones: login failed (use an app password), "macOS is blocking access to Mail's folder" (grant Full Disk Access), iCloud rejecting large uploads (use **Large messages**).

More: [Is Pigeonhole safe to trust?](docs/trust.md)

## Uninstall

Quit Pigeonhole and drag it from Applications to the Bin. To also remove its data, delete `~/.icloud_dedupe`, and the Pigeonhole items in Keychain Access if you ticked "Remember".

## Licence

Free to use for personal use, provided as is without warranty. Copyright David Defranceski. See [LICENSE](LICENSE).
