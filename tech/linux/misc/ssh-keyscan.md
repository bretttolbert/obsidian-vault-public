# ssh-keyscan

ssh-keyscan is a utility for gathering the public ssh host keys of a number of hosts. It was designed to aid in building and verifying `known_hosts` files.

Note: Whether `ssh-keyscan` returns the entire public key or just the fingerprint of the public key seems to be dependent upon the configuration. 

###### Get public SSH key from a remote host
```bash
$ # Scan remote host for public SSH key (add -H for hashed for use with hashed known_hosts file)
$ ssh-keyscan -t rsa 192.168.0.1 > key.pub 2> /dev/null

$ cat key.pub 
192.168.0.119 ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCXOTEGCbWuTBcaW9FjkufDC1ItOy5NephXO36ypJxFG6PIBGCkABq7YngMGTcUJ/sUs+j4JpA1/GUx5j2txgtGLJPLVwH4LDpc0sHtXilIOFiAR9QDMbv4zP1kX9VkvgHltCTmQb881bthxQMHa7qmsjcv1qAfUWmtfhZEjOiPAKZavrEXyCT0vSwoFxQOFsSCnlY5OFhU3gFLY0LTbGjc05+kii7TWITHOHpBqdFIZebeYxXwUxoFxh3wGb5ycgfc9VHnrR9CIj0jGEbqAKZnqpyd3zV/dwytH1/uc2imZdlKOleyV+Irz05bCuxXaZodXkm5ZuMQCbsMM9e3ase4rYQQVqGJylqx6P8WFGzVJLNnrdj0Ya8tzC6hDdWyEFE8u9u4cOhLE4oPwDPuvr5A90nu9c5sC2XpxAhJuatxv5OMb2bevAoow/eWu6ensyb2UX0VF6ob43p5cR5HhV4o3qIAWEpYf6MDUmHrbrAH+yEUuU2OJy0L3DDc6mMkapk=

$ # Use `cut` to remove IP/hostname
$ cat key.pub | cut -d' ' -f2,3
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCXOTEGCbWuTBcaW9FjkufDC1ItOy5NephXO36ypJxFG6PIBGCkABq7YngMGTcUJ/sUs+j4JpA1/GUx5j2txgtGLJPLVwH4LDpc0sHtXilIOFiAR9QDMbv4zP1kX9VkvgHltCTmQb881bthxQMHa7qmsjcv1qAfUWmtfhZEjOiPAKZavrEXyCT0vSwoFxQOFsSCnlY5OFhU3gFLY0LTbGjc05+kii7TWITHOHpBqdFIZebeYxXwUxoFxh3wGb5ycgfc9VHnrR9CIj0jGEbqAKZnqpyd3zV/dwytH1/uc2imZdlKOleyV+Irz05bCuxXaZodXkm5ZuMQCbsMM9e3ase4rYQQVqGJylqx6P8WFGzVJLNnrdj0Ya8tzC6hDdWyEFE8u9u4cOhLE4oPwDPuvr5A90nu9c5sC2XpxAhJuatxv5OMb2bevAoow/eWu6ensyb2UX0VF6ob43p5cR5HhV4o3qIAWEpYf6MDUmHrbrAH+yEUuU2OJy0L3DDc6mMkapk=

$ # Use `cut` to remove IP/hostname and append to `authorized_keys` (allows remote host to login without password!)
$ cat key.pub | cut -d' ' -f2,3 >> ~/.ssh/authorized_keys
```

