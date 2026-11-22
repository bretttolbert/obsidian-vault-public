# virtualbox

###### Change the UUID of a .vdi image
```bash
VBoxManage internalcommands sethduuid BuildDrive160GB.vdi
```

###### Add linux guest user to vbox shared folders group
```bash
usermod -a -G vboxsf brett
```
