# aspell

###### Generate a .dic (dictionary) file for use with PyCharm or other InteliJ IDE

```bash
aspell --lang fr dump master | aspell --lang fr expand | tr ' ' '\n' > french.dic
```
