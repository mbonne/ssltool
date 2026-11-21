# ssltool

Menu-driven helper for everyday OpenSSL tasks: making CSRs, checking that a key and certificate belong together, and inspecting certificates.

`ssltools` wraps the OpenSSL commands you look up every time. It is for admins who occasionally need to request or check a certificate and don't want to remember the flags.

## Menu

| Option | What it does |
|---|---|
| 1. Generate CSR | New CSR, renew from an existing one, or build from an existing config. Creates the private key and `.cnf` alongside it. |
| 2. Validate Cert Hash | Compares the modulus hash of a CSR, certificate and private key to confirm they match. |
| 3. Show CSR Details | Prints and verifies a CSR's contents. |
| 4. Check SSL On Host | Fetches and prints the certificate a server presents on port 443. |
| 5. Print Certificate to Terminal | Prints a CSR, private key or public certificate and copies it to the clipboard. |

Generated `.cnf`, `.csr` and `.key` files are stored in `$HOME/.config/sslTool`.

## What it runs

```sh
# Validate Cert Hash
openssl req  -noout -modulus -in "$csrFile" | openssl md5
openssl x509 -noout -modulus -in "$pubKey"  | openssl md5
openssl rsa  -noout -modulus -in "$privKey" | openssl md5

# Show CSR Details
openssl req -text -noout -verify -in "$csrFile"

# Check SSL On Host
openssl s_client -showcerts -servername "$hostURL" -connect "$hostURL":443 2>/dev/null \
  | openssl x509 -inform pem -noout -text
```

## Requirements

- macOS (uses `pbcopy` and BSD `stat`)
- bash, `openssl`, `curl`, `dig`

## Install

```sh
mkdir -p "$HOME/bin"
ln -s "/path/to/ssltool/ssltools" "$HOME/bin/ssltools"
```

Make sure `$HOME/bin` is on your `PATH`, then run:

```sh
ssltools
```

## Caution

Option 5 copies a private key to the clipboard when you print one. Clear your clipboard afterwards, and keep `$HOME/.config/sslTool` private since it holds your keys.

## Known limitations

- Wildcard names (`*`) are not yet handled in generated file names.

## License

GPL-3.0. See [LICENSE](LICENSE).
