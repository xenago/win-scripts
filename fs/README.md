# fs

Filesystem-related.

## Long paths

By default, `MAX_PATH` is `260` characters. On Windows 10+ this can be safely extended to a more reasonable 32k chars with the registry or Group Policy.

### Enabling long paths

This can be done in the registry on Home editions or Group Policy on all other editions. Use `gpedit.msc` if available.

#### Registry

Set the 32-bit DWORD at  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem\LongPathsEnabled` to `1`.

#### Group Policy

Set  `Computer Configuration > Administrative Templates > System > Filesystem > Enable Win32 long paths` to `Enabled`.

### Workarounds

Sometimes, simply does not work and certain paths are still borked and workarounds are required.

#### UNC prefix

Sometimes preceding the path with the UNC prefix will work, e.g.

```
\\?\T:\path\that\is\long\to\file.txt
```

#### Total Commander

Total Commander is also able to work around this problem and can be helpful GUI tool when dealing with wonky Windows-unfriendly paths created by non-native tools. Always keep a portable copy on hand in your applications folder.
