# Troubleshooting

**"Login failed"**
Use an [app-specific password](app-passwords.md), not your normal password. Check the address is exactly right.

**"macOS is blocking access to Mail's folder"** (Local mail)
Give Pigeonhole Full Disk Access: System Settings > Privacy & Security > Full Disk Access > switch on Pigeonhole (press **+** if missing), then quit and reopen it.

**Pigeonhole says a task is running and greys out buttons**
Only one task runs at a time. Open the tab with the pulsing dot to watch it or press **Stop**.

**A merge or move seems slow**
iCloud handles roughly 5 to 10 messages a second. The task panel shows the speed and an estimate of the time left. Large moves can take an hour; it is safe to leave it running. If it shows "No progress for 5 minutes", press **Stop** (what already moved is kept in History) and start again.

**Mail shows "APPEND … TOOBIG" when moving mail between accounts**
iCloud rejects messages above about 40 MB. Use **Tidy up > Large messages** to find them, then save their attachments to disk and strip them from the email.

**A duplicate group is marked "Sizes differ"**
The copies share a Message-ID but differ in size (for example, one had its attachment removed). They are left alone by default. Change **Copies count as identical when their sizes are within** in Review to include them.

**"Prefer filed folders" didn't change anything**
It only changes groups where one copy sits in a deeper sub-folder than the other. A message in INBOX and the account's top-level folder counts as the same depth.

**Undo says some messages weren't found**
Messages without a Message-ID can't be found again once moved. Messages already emptied from Trash can't be restored.

**Pigeonhole won't open ("cannot be verified")**
Download the DMG again from the [Releases page](https://github.com/daviddef/PigeonHole-Public-/releases), and open it from there. If it still fails, tell us your macOS version.

**Where are my settings?**
`~/.icloud_dedupe` (Help > Open Pigeonhole's data folder). Quit Pigeonhole before editing anything in it.

## Reporting a problem

Open an [issue](https://github.com/daviddef/PigeonHole-Public-/issues) with your macOS version and what you were doing. Please don't include email addresses or passwords.
