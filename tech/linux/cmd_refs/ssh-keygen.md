# ssh-keygen

## See Also
- [ssh](./ssh.md)
- [ssh-copy-id](./ssh-copy-id.md)
- [openssl](./openssl.md)
- [openssl enc](./openssl_enc.md)
- [scp](./scp.md)

###### List md5 fingerprints of SSH key(s) (works with individual keys as well as `authorized_keys` and `known_hosts` files)
```bash
ssh-keygen -E md5 -lf {filename}
```

###### Remove keys from `known_hosts` file
```bash
ssh-keygen -R {host}
```

###### Search a hashed `known_hosts` file for the given host
```bash
ssh-keygen -F 192.168.0.1 -f ~/.ssh/known_hosts
```

