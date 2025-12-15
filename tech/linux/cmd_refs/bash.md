# bash

## See also
- [expr](./expr.md)

###### List all exported variables and functions
```bash
export -p
```

###### Export a function by name
```bash
export -f name
```

###### Bash `test` command

[IBM - Tutorial - Bash test and comparison functions](https://www.ibm.com/developerworks/library/l-bash-test/index.html)

###### Test operators
- `-z` non-zero string length
- `-o` logical or
- `-d` directory
- `-f` regular file
- `-e` exists
- `-s` non-empty

###### Test operator `-z`
The unary operator -z tests for a null string, while -n or no operator at all returns True if a string is not empty. Example:
```bash
$ test -z "foo" && echo "foo"
$ test -z "" && echo "foo"
foo
```

###### Show help info for all Bash test flags
```bash
help test
```

###### See the exit code returned by the previous command
```bash
$?
```

