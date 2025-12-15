# windows

###### List IP interfaces
```bat
ipconfig /all
```

###### Show NIC info
```bat
netsh bridge show adapter
```
###### Copy a directory with robocopy, don't purge files that don't exist locally
```bat
robocopy N: M: /XD *RECYCLE.BIN /R:3 /E
```
- `N:` source path
- `M:` destination path
- `/XD *RECYCLE.BIN` exclude directories with names ending with *RECYCLE.BIN*
- `/R:3` 3 max retries on failed copy
- `/W:10` 10 second wait time on failed copy
- `/E` copy subdirectories, including **e**mpty ones

###### Mirror a directory with robocopy, purging files that don't exist locally
```bat
robocopy N: M: /XD *RECYCLE.BIN /R:3 /W:10 /MIR
```
- `/MIR` mirror the directory (delete files on dest that don't exist on source) (`/MIR` is `/E` plus `/PURGE`)

###### Assign disk drive letter
```bat
diskpart
list volume
select volume 1
assign letter=D
```

