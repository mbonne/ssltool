# ssltool
CLI tool which uses builtin binary, to create private key, csr, validate md5 hash of certs


To run the tool, simply execute script.

Then select from the menu.

Menu Tree:
(More options and functions when I work out whats useful and how to implement it...)

1) Generate CSR


2) Validate Cert Hash


3) Show CSR Details


4) Check SSL On Host
    Returns output from the following commands
      openssl s_client -showcerts -servername "$hostURL" -connect "$hostURL":443 2>/dev/null | openssl x509 -inform pem -noout -text

5) Quit
    uh...Quits the script.
