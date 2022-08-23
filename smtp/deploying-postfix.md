# Deploying Postfix (SMTP)

This was performed on a Raspberry Pi using iCloud as my SMTP server (smtp.mail.me.com). This will need to be changed if using a different mail service.

## Installation

```bash
sudo apt install mailutils postfix libsasl2-modules
```

## Create App Password

Navigate to [appleid.apple.com](https://appleid.apple.com) and create a new app password to be used for the SMTP authentication.

## SASL Configuration

Modify the uppercase values below before running, using the app password generated above as the PASSWORD value.

```bash
sudo echo "[smtp.mail.me.com]:587 MYACCOUNT@icloud.com:PASSWORD" > /etc/postfix/sasl_passwd
sudo chmod 600 /etc/postfix/sasl_passwd
sudo postmap /etc/postfix/sasl_passwd
```

## Main.cf Configuration

Add the following settings to the end of the `main.cf` file and make sure to delete any previous `relayhost =` lines.

```
relayhost = [smtp.mail.me.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_security_level = encrypt
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
```

## Restart postfix

```bash
sudo systemctl restart postfix
```

## Test mail

Modify the uppercase values below before running. Note: in the case of iCloud mail, the From address must be one of your addresses configured in your settings. If not, emails will not be sent.

```bash
mail -s "My Test Email" -aFrom:"MYACCOUNT@icloud.com" TOADDRESS <<< "Test email"
```
