Python S/MIME Toolkit
=====================

This library implements a S/MIME handler. In this first version, it can only
encrypt S/MIME messages using a public RSA key, in AES128-CBC, AES192-CBC or
AES256-CBC modes.

The ASN.1 implementation does not depend on pyasn1, as it showed too broken for
creating and reading CMS (Cryptographic Message Syntax). Instead, the [Google's
certificate transparency project](https://www.certificate-transparency.org/)
was used in this project.

This implementation uses pycrypto instead of OpenSSL, so everything is 'pure
python'.


Example:
--------

```python
import sys
import smime

message = [
    'To: "Alice" <alice@foo.com>',
    'From: "Bob" <bob@bar.com>',
    'Subject: A message from python',
    '',
    'Now you see me.'
]

with open('alice-public-key.pem', 'rb') in pem
    print(smime.encrypt('\n'.join(message), pem.read()))
```

Output:

```
To: "Alice" <alice@foo.com>
From: "Bob" <bob@bar.com>
Subject: Received SMS from Twilio
MIME-Version: 1.0
Content-Type: application/pkcs7-mime; smime-type=enveloped-data; name=smime.p7m
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename=smime.p7m

<base64-enveloped-data>
```
