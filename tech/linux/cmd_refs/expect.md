# Expect

###### Expect script to `scp` all files in the current directory

```bash
#!/usr/bin/expect -f

spawn scp -r . admin@10.17.127.11:~/AudioPathVerification/
#######################
expect {
  -re ".*es.*o.*" {
    exp_send "yes\r"
    exp_continue
  }
  -re ".*sword.*" {
    exp_send "H81Fv5G2\r"
  }
}
interact
```
