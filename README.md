# Text Encryptor

Encrypt and decrypt text in your browser with a passphrase using the Web Crypto API. The output is a portable base64 blob. Nothing leaves your browser.

## Live demo

https://0xelitesystem.github.io/text-encryptor/

## Features

- Encrypt mode: turn text plus a passphrase into a single portable base64 ciphertext blob.
- Decrypt mode: turn a blob plus the passphrase back into the original text.
- Authenticated encryption with AES-256-GCM, so a wrong passphrase or altered ciphertext is detected and rejected with a clear error.
- Key stretching with PBKDF2 over SHA-256 at a high iteration count.
- Fresh random salt and IV per encryption.
- Copy button, dark mode toggle, keyboard friendly.
- One file, no external dependencies, works offline.

## How it works

The scheme uses the standard browser crypto primitives through `crypto.subtle`. It never rolls a custom cipher.

- Cipher: AES-256-GCM (authenticated encryption).
- Key derivation: PBKDF2 with SHA-256 and 250000 iterations.
- Salt: 16 random bytes, generated fresh for every encryption and used to derive the key.
- IV: 12 random bytes, generated fresh for every encryption and used by GCM.
- Output layout: salt, then IV, then ciphertext, concatenated and encoded as base64. Everything needed to decrypt (except the passphrase) is prepended to the blob.

Because GCM is authenticated, decrypting with the wrong passphrase (or a modified blob) fails the integrity check and returns an explicit error rather than garbage.

## Privacy

Everything runs in your browser. Your text, your passphrase, and the ciphertext never leave your machine. There are no external requests, no analytics, and no tracking.

Note: a forgotten passphrase means the data is unrecoverable. There is no reset and no backdoor. Keep your passphrase safe.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
