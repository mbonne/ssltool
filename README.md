# ssltool

## CLI tool assist with OpenSSL operations

How to use:
To run the tool, simply execute script:

```bash
./ssltools
```

Then select what you want from the menu.

<br>

## Menu Tree

>(More options and functions when I work out whats useful and how to implement it...)

<br>

### Option 1) Generate CSR

>The following location `$HOME/.conf/sslTool` is used for storing `.cnf`, `.csr` and `.key` files.

- New CSR
- Renew from existing

<br>

### Option 2) Validate Cert Hash

>This will take your CSR, Public and Private key/Certificate files and show you the hash vaule of each.

```bash
openssl req -noout -modulus -in "$csrFile" | openssl md5
openssl x509 -noout -modulus -in "$pubKey" | openssl md5
openssl rsa -noout -modulus -in "$privKey" | openssl md5
```

<br>

### Option 3) Show CSR Details

>Prints the details of your selected .csr file.

```bash
openssl req -text -noout -verify -in "$csrFile"
```

<br>

### Option 4) Check SSL On Host

>Returns output from the following commands

```bash
openssl s_client -showcerts -servername "$hostURL" -connect "$hostURL":443 2>/dev/null | openssl x509 -inform pem -noout -text
```

<br>

### 5) Quit

>uh...Quits the script.
