# Encrypt .env before pushing to Git

Encrypt a `.env` file before committing it to Git:

```bash
gpg -a -c local.env
```

This asks for a passphrase and creates an encrypted text file, usually `local.env.asc`. The content is protected, so the repo only stores the encrypted version.

To restore it later:

```bash
gpg -o local.env -d local.env.asc
```

This decrypts the file back to its original `.env` form using the same passphrase.

In short: commit the encrypted file, keep the real `.env` local, and never store the secret in Git.