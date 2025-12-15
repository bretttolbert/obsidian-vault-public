# GPG

## See also
- [openssl](./openssl.md)

###### List keys
```bash
gpg --list-keys --keyid-format short
```

###### List secret keys
```bash
gpg --list-secret-keys --keyid-format short
```

###### Export public key
```bash
gpg --armor --export user@mail.com > mynewkey.asc
```

###### Delete a key pair
```bash
gpg --delete-secret-keys ID
gpg --deley-key ID
```

###### Generate a new key pair with full options:
```bash
gpg --full-gen-key
```