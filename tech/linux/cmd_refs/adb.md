# android debug bridge (adb)

###### List devices
```bash
./adb devices
```

###### What if USB debugging keeps disconnecting
Reboot phone, disabled USB debugging then reenable it.

###### What if `adb devices` lists device as *unathorized*
Look for a pop-up on phone to allow USB debugging

###### Reset android media scan database
- Must enable developer mode first
- Can be executed via USB debugging or LADB
```
pm clear com.android.providers.media.module
```

###### Open shell
```bash
./adb shell
```

###### My IMEI
```
3554 8511 0441 106
```


