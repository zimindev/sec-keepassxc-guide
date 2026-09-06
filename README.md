# 🔐 KeePassXC Security Guide

## ✅ What is KeePassXC?

**KeePassXC** is a free and open-source password manager that securely stores passwords, credentials, secure notes, TOTP secrets, and other sensitive information in an encrypted database.

Instead of remembering dozens of passwords, you only need to protect **one strong master password**.

### 🔑 Basic Security Model

```text
                 ┌─────────────────────┐
                 │   Strong Master     │
                 │      Password       │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    KeePassXC        │
                 │  Encrypted Database │
                 └──────────┬──────────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
          Passwords       TOTP        Secure Notes
              │             │             │
              └─────────────┼─────────────┘
                            ▼
                    Protected Accounts
```

---

# 🛡️ 1. Use a Strong Master Password

Your **master password** protects the entire KeePassXC database.

If someone obtains your database file, the master password is one of the primary protections preventing them from opening it.

### Recommended

Use a long, unique passphrase:

```text
River-Moon-Glass-Orange-Planet-47
```

Or a randomly generated password:

```text
v7!Qm2#Lp9@Tx4$Nz8&Kr5
```

These are **examples only**. Never use passwords published in documentation.

### Recommended minimum

```text
Length:        16+ characters
Better:        20–30+ characters
Unique:        Yes
Random:        Preferably
Reused:        Never
```

### ❌ Avoid

```text
password123
qwerty123
admin123
Welcome123
YourName2026
CompanyName2026
```

---

# 🔒 2. Use KeePassXC's Database Encryption

KeePassXC uses an encrypted database format to protect stored credentials.

Your database should normally be stored as:

```text
*.kdbx
```

Example:

```text
Passwords.kdbx
```

Treat the `.kdbx` file as **sensitive data**.

Even though the database is encrypted, you should still protect it from unauthorized access.

---

# 🧩 3. Use a Key File for Additional Protection

KeePassXC supports a **key file** as an additional database unlock factor.

You can configure:

```text
Master Password + Key File
```

instead of only:

```text
Master Password
```

### Security model

```text
Database
   │
   ├── Master Password
   │
   └── Key File
          │
          ▼
       Unlock
```

A stolen database without the key file is much harder to attack.

### ⚠️ Important

Do **not** store the key file next to the database.

Bad:

```text
USB/
├── Passwords.kdbx
└── Passwords.key
```

Better:

```text
Cloud Backup/
└── Passwords.kdbx

Offline USB/
└── Passwords.key
```

Keep independent backups of the key file.

### 🚨 Critical Warning

If you lose the key file **and** cannot unlock the database another way, you may permanently lose access to your passwords.

Always maintain a secure backup.

---

# 🧠 4. Consider Using a Key File Carefully

A key file can significantly strengthen your security model, but it also increases the risk of **self-lockout**.

Before using one, make sure you understand:

```text
Database backup
       +
Key file backup
       +
Master password
       =
Recoverable password vault
```

Never rely on a single copy of either the database or key file.

---

# 🔑 5. Generate Passwords with KeePassXC

Do not manually create passwords for every account.

Use KeePassXC's password generator.

Example configuration:

```text
Length:        24+
Uppercase:     Yes
Lowercase:     Yes
Numbers:       Yes
Special:       Yes
```

Example generated password:

```text
G4@xP9!rL2#Vm7$Qz8^Nt6
```

Another example:

```text
F7@qL2#vN9!xR4$kT8%pM6&zC3
```

These examples are for demonstration only.

### 🎯 Goal

Every important account should have a **different password**.

```text
Google     → Password A
GitHub     → Password B
Cloudflare → Password C
Email      → Password D
Router     → Password E
Server     → Password F
```

---

# 🚫 6. Never Reuse Passwords

Password reuse creates a chain reaction.

```text
Website A compromised
        │
        ▼
Password leaked
        │
        ▼
Attacker tries same password
        │
        ├── Email
        ├── GitHub
        ├── Cloudflare
        ├── Banking
        └── Other services
```

Use unique credentials for every service.

---

# 🔐 7. Protect Your Master Password

Never store your master password:

```text
❌ In a text file
❌ In an email
❌ In a Git repository
❌ In a public cloud document
❌ In browser bookmarks
❌ In screenshots
❌ In chat messages
```

Do not put it inside:

```text
passwords.txt
credentials.txt
notes.txt
README.md
.env
```

### Best practice

Memorize your master password.

If you need a physical recovery method, keep it offline in a secure location.

---

# 💾 8. Back Up Your Database

Your KeePassXC database is extremely important.

If your computer fails and you have no backup:

```text
Disk failure
     ↓
Database lost
     ↓
Passwords lost
```

Maintain multiple backups.

### Recommended structure

```text
Primary
└── ~/Documents/Passwords.kdbx

Backup 1
└── Encrypted USB

Backup 2
└── Secure cloud storage

Backup 3
└── Offline backup
```

---

# ☁️ 9. Be Careful with Cloud Synchronization

You can synchronize your `.kdbx` database using cloud storage.

However, remember:

```text
Cloud storage
      ↓
Encrypted KDBX database
      ↓
Strong master password
      ↓
Protected vault
```

Never upload unencrypted password files such as:

```text
passwords.txt
passwords.csv
credentials.txt
```

### ⚠️ Important

A `.csv` export from a password manager is generally **not encrypted**.

Delete plaintext exports immediately after use.

---

# 📦 10. Secure Database Backups

Backups should receive the same security considerations as the original database.

Example:

```text
Passwords.kdbx
Passwords-backup.kdbx
Passwords-old.kdbx
```

Avoid leaving dozens of uncontrolled copies.

Use a clear backup strategy:

```text
Primary database
        │
        ├── Encrypted backup
        ├── Offline backup
        └── Recovery backup
```

Periodically verify that backups can actually be opened.

---

# 🧹 11. Delete Plaintext Exports

If you export your database to CSV:

```text
Passwords.csv
```

the passwords may be stored in plaintext.

After importing or transferring the data:

```bash
rm -f Passwords.csv
```

Also empty the desktop environment's trash/recycle bin if appropriate.

### ⚠️ Remember

Deleting a plaintext file does not always guarantee that every trace is immediately unrecoverable, especially on SSDs, snapshots, backups, or synchronized storage.

Avoid creating plaintext exports unless absolutely necessary.

---

# 🔒 12. Lock KeePassXC When Away

Always lock the database when you leave your computer.

Use:

```text
Lock Database
```

instead of leaving the vault open indefinitely.

Recommended:

```text
Computer idle
      ↓
Short inactivity period
      ↓
KeePassXC locks
      ↓
Master authentication required
```

Also enable automatic database locking where appropriate.

---

# 🖥️ 13. Secure the Operating System

KeePassXC cannot compensate for a compromised operating system.

Keep your system updated.

### Arch Linux

```bash
sudo pacman -Syu
```

### Debian / Ubuntu

```bash
sudo apt update
sudo apt upgrade
```

### Fedora

```bash
sudo dnf upgrade
```

Use:

```text
✓ Full-disk encryption
✓ Strong OS password
✓ Automatic updates
✓ Screen locking
✓ Firewall
✓ Trusted software sources
✓ Secure boot where appropriate
```

---

# 🦠 14. Protect Against Malware

A password manager is not a complete security solution.

If malware controls your computer, an attacker may potentially capture credentials while they are being entered or used.

Use:

```text
OS updates
+
Firewall
+
Trusted software
+
Browser security
+
Anti-malware protection
+
Least privilege
```

Avoid installing unknown software or running suspicious scripts as root/administrator.

---

# 🌐 15. Be Careful with Browser Integration

KeePassXC can integrate with supported browsers.

Browser integration is convenient, but it increases the interaction between your browser and password manager.

Only enable it for browsers and profiles you trust.

Review:

```text
Browser extensions
Native messaging
Allowed domains
Auto-fill settings
```

### Best practice

Use auto-fill carefully and verify the website domain before submitting credentials.

For example:

```text
github.com       ✅
accounts.google.com  ✅

github-login.example.com  ❌
google-security.example.com ❌
```

---

# 🎣 16. Protect Against Phishing

KeePassXC can store the correct password, but **you still need to verify the website**.

Before entering credentials:

```text
Check domain
      ↓
Check HTTPS
      ↓
Check spelling
      ↓
Check certificate/browser warning
      ↓
Authenticate
```

Example:

```text
https://github.com
```

is different from:

```text
https://github-login.example.com
```

Never enter your credentials simply because a page looks identical to the real website.

---

# 🔐 17. Store TOTP Secrets Securely

KeePassXC can also store TOTP credentials.

For example:

```text
GitHub
├── Username
├── Password
└── TOTP Secret
```

This can be convenient because your authentication data can remain inside the encrypted vault.

### However

Do not automatically place **every authentication factor in the same location** if your threat model requires strong separation.

For highly sensitive accounts, consider:

```text
Password → KeePassXC
TOTP      → Separate authenticator
Recovery  → Offline backup
```

This provides better separation between authentication factors.

---

# 🔑 18. Use MFA for Important Accounts

Password managers protect passwords.

MFA protects accounts even if passwords are compromised.

Recommended:

```text
Password
    +
MFA
    +
Recovery codes
```

Prefer:

```text
Passkeys
Security keys
Authenticator TOTP
```

over:

```text
SMS
```

when stronger options are available.

---

# 🗝️ 19. Protect Recovery Codes

Recovery codes are extremely sensitive.

Example:

```text
1234-5678
9271-4632
5518-2049
```

These are only examples.

Store real recovery codes securely.

Possible options:

```text
Encrypted password manager
Offline encrypted storage
Secure physical backup
```

Do not publish them or store them in public repositories.

---

# 📁 20. Never Store KeePass Databases in Git

Never commit:

```text
Passwords.kdbx
Passwords.csv
credentials.txt
secrets.txt
```

to GitHub or another public repository.

Bad:

```bash
git add Passwords.kdbx
git commit -m "add passwords"
git push
```

Even if you delete the file later, it may remain in Git history.

### Add sensitive files to `.gitignore`

```gitignore
*.kdbx
*.key
*.csv
credentials.txt
passwords.txt
secrets.txt
```

---

# 🔍 21. Regularly Audit Your Password Database

Periodically review:

```text
✓ Reused passwords
✓ Weak passwords
✓ Old passwords
✓ Duplicate accounts
✓ Unused accounts
✓ Old recovery codes
✓ Old TOTP secrets
✓ Old database entries
```

Remove credentials for accounts that no longer exist.

---

# 🧪 22. Test Your Backups

A backup that cannot be restored is not a reliable backup.

Periodically test:

```text
Backup exists
      ↓
Copy backup to test location
      ↓
Open with KeePassXC
      ↓
Unlock successfully
      ↓
Verify several entries
```

Do not modify the original backup during testing.

---

# 🛡️ 23. Recommended KeePassXC Security Configuration

| Feature             | Recommendation                     |
| ------------------- | ---------------------------------- |
| Master password     | 20+ characters                     |
| Password reuse      | Never                              |
| Database format     | KDBX                               |
| Key file            | Optional, useful for high security |
| Database backup     | Multiple copies                    |
| Cloud backup        | Encrypted database only            |
| Plaintext CSV       | Avoid                              |
| Auto-lock           | Enabled                            |
| OS screen lock      | Enabled                            |
| Disk encryption     | Recommended                        |
| Browser integration | Only when needed                   |
| MFA                 | Enabled                            |
| TOTP                | Prefer over SMS                    |
| Passkeys            | Prefer where available             |
| Recovery codes      | Stored securely                    |
| Git repository      | Never store secrets                |

---

# 🔐 24. Recommended High-Security Setup

A strong personal setup could look like:

```text
                 ┌────────────────────┐
                 │   Master Password  │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │    Key File        │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │ KeePassXC Database  │
                 │      .kdbx          │
                 └─────────┬──────────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
         Passwords        TOTP       Secure Notes
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                    Protected Accounts
```

Backup:

```text
              KeePassXC Database
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Local Backup   USB Backup   Cloud Backup
          │            │            │
          └────────────┼────────────┘
                       ▼
                 Recovery Plan
```

---

# 🚨 25. What to Do If Your Database Is Compromised

If you believe your `.kdbx` database or master password has been exposed:

### Immediately:

```text
1. Secure your computer
2. Change the KeePassXC master password
3. Change critical account passwords
4. Revoke active sessions
5. Rotate API tokens
6. Replace SSH keys if necessary
7. Regenerate TOTP secrets where appropriate
8. Replace recovery codes
9. Check account activity
10. Create a new secure database if required
```

Prioritize:

```text
Email
Cloud accounts
Password manager
GitHub
Financial accounts
Server infrastructure
Domain registrar
Cloudflare
```

---

# 🧰 26. KeePassXC Security Checklist

### 🔐 Master Password

* [ ] 20+ characters
* [ ] Unique
* [ ] Never reused
* [ ] Not stored in plaintext
* [ ] Not shared with anyone

### 🗄️ Database

* [ ] `.kdbx` database encrypted
* [ ] Regular backups
* [ ] Backups tested
* [ ] No plaintext exports
* [ ] No database in Git

### 🔑 Key File

* [ ] Key file stored separately
* [ ] Backup exists
* [ ] Recovery procedure tested
* [ ] Key file never uploaded publicly

### 💻 Computer

* [ ] OS updated
* [ ] Disk encryption enabled
* [ ] Screen lock enabled
* [ ] Firewall enabled
* [ ] Unknown software avoided

### 🌐 Accounts

* [ ] Unique passwords
* [ ] MFA enabled
* [ ] Passkeys used where available
* [ ] Recovery codes protected
* [ ] Old sessions revoked

### 🌍 Browser

* [ ] Trusted browser only
* [ ] Minimal extensions
* [ ] Browser integration configured carefully
* [ ] Domains verified before login

---

# 🏆 27. Golden Rules

```text
1. Protect the master password.
2. Use unique passwords for every account.
3. Prefer long passwords over short complex passwords.
4. Keep your .kdbx database encrypted.
5. Back up the database.
6. Back up the key file if you use one.
7. Keep backups independent.
8. Never store plaintext password exports.
9. Never commit secrets to Git.
10. Enable MFA on important accounts.
11. Prefer passkeys/security keys where available.
12. Lock KeePassXC when not in use.
13. Keep your operating system updated.
14. Be careful with browser integration.
15. Verify domains before logging in.
16. Test your recovery process.
```

---

# 🔒 28. Recommended Security Architecture

For a strong personal security setup:

```text
                 ┌───────────────────────┐
                 │   Secure Computer     │
                 │                       │
                 │ Full-Disk Encryption  │
                 │ Firewall              │
                 │ Updates               │
                 └───────────┬───────────┘
                             │
                             ▼
                  ┌────────────────────┐
                  │     KeePassXC      │
                  │                    │
                  │ Master Password    │
                  │ + Key File         │
                  │ + Encrypted KDBX   │
                  └─────────┬──────────┘
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
        Unique Passwords   TOTP        Secure Notes
             │              │
             └──────────────┼──────────────┘
                            ▼
                     Online Accounts
                            │
                            ▼
                    MFA / Passkeys
```

---

# 📌 Final Recommendation

A secure KeePassXC setup should follow this principle:

```text
Strong Master Password
          +
Encrypted Database
          +
Secure Backups
          +
Unique Passwords
          +
MFA / Passkeys
          +
Secure Operating System
          +
Phishing Protection
          =
Strong Password Security
```

KeePassXC is only one layer of your security architecture. The strongest setup combines a secure password manager with **unique credentials, MFA/passkeys, encrypted storage, reliable backups, and a properly secured operating system**.

---

## 🔗 Official Resources

* **KeePassXC:** https://keepassxc.org/
* **KeePassXC Documentation:** https://keepassxc.org/docs/
* **KeePassXC Downloads:** https://keepassxc.org/download/
* **KeePassXC GitHub:** https://github.com/keepassxreboot/keepassxc
