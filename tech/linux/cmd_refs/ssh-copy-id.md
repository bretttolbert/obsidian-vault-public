# ssh-copy-id

## See Also
- [ssh](./ssh.md)
- [ssh-keygen](./ssh-keygen.md)
- [openssl](./openssl.md)
- [openssl enc](./openssl_enc.md)
- [scp](./scp.md)

`ssh-copy-id` is used to install the local public SSH key as an authorized key on a remote SSH server. 
This allows login without password.

###### `ssh-copy-id` example
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```

`-i identity_file` Use only the key(s) contained in `identify_file` (rather than looking for identities via ssh-add(1) or in the `default_ID_file`.)

