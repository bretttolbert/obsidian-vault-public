# screen

###### List screen sessions
```bash
screen -ls
```

###### Detach from an attached screen session
```bash
Ctrl + a + d
```

###### Reattach a screen
```bash
screen -r {id}
```

###### Kill a detached screen session
```bash
screen -SX {id} quit
```
- `-S` sessionname
- `-X` send the specified command
- `{id}` the detached screen session id
- `quit` this command terminates the screen session

