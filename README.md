## Decrypting a backup file (command line)

You can always recover your secret from a backup file using only:

- Your **backup JSON file**
- Your **Keypsafe password** (same one you log in with)
- Your **recovery key** (the Base64URL string)

---

### 1. Requirements

- [Node.js](https://nodejs.org/) installed (version 18+ recommended)
- Git installed

---

### 2. Download your backup

In the Keypsafe app:

1. Go to **Settings → Download backup**
2. Save the file somewhere safe, e.g.
   `~/Downloads/keypsafe-vault-....json`

---

### 3. Clone the repo

```bash
git clone https://github.com/ssc256/keypsafe-recovery.git
cd keypsafe-recovery
```

### 4. Run the decrypt script

You must choose where the output goes. Either pass `--output` to write to a file (recommended), or `--stdout` to print to the terminal.

**Recommended — save to a file:**

```bash
node recover.js /full/path/to/backup.json --output secret.txt
```

The secret is written to `secret.txt` and never appears on screen. Delete or move the file to a secure location when you are done.

**Alternative — print to terminal:**

```bash
node recover.js /full/path/to/backup.json --stdout
```

Either way, the script will prompt you for your password and recovery key. Neither will be visible as you type:

```
Password:
Recovery key (Base64URL):
```

When printing to the terminal, the script pauses after showing your secret and clears the screen (including scrollback) when you press Enter.

---

## Security tips

- Run this on a machine you trust.
- Never pass your password or recovery key as command-line arguments — the script always prompts for them interactively.
- After saving to a file, delete it when done: `rm secret.txt`
- When printing to the terminal, close the terminal window afterwards as an extra precaution.
