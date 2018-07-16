[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [File Permissions](file-permissions.md)

# File & Directory Permissions in Linux

The `chmod` command is used to control the access permissions for directories. We can use the octal notation to set permissions. To describe the octal notation, we can add permission values to obtain new, combined (octal) values.

Permission values:

- 1 – able to execute (_x_)
- 2 – able to write (_w_)
- 4 – able to read (_r_)

The octal number is the sum of the permission values, for example:

- 3 (1+2) – able to execute and write
- 6 (2+4) – able to write and read

The meaning of the r, w, and x attributes is different:

- **r** - Allows the contents of the directory to be listed if the x attribute is also set.
- **w** - Allows files within the directory to be created, deleted, or renamed if the x attribute is also set.
- **x** - Allows a directory to be entered (i.e. `cd dir`).

There are three digits in a `chmod` permission. The first digit represents the permissions of the user, the second represents the group, and the third represents global permissions. So if a file has permissions `754`, the user can read, write, and execute; the group can read and execute, while all other users can only read.

Permissions my be interpreted and set numerically (640) or symbolically (wr-).

Permission `600` is a common setting for data files that the owner wants to keep private. The owner may read and write a file. All others have no rights.

_`600` is equivalent to `rw-------`._

If you have another setting configured for your _private data file_, please run the `chmod` command to set it to `600`.

```bash
sudo chmod filename 600
```

**This table covers the common settings, those beginning with "7" are typically used with programs (since they enable execution) and the rest are for other kinds of files.**

Value | Meaning     | Description
:---: | ----------- | ----------------------------------------
 777  | `rwxrwxrwx` | No restrictions on permissions. Anybody may do anything. Not a desirable setting.
 755  | `rwxr-xr-x` | The file's owner may read, write, and execute the file. All others may read and execute the file. This setting is common for programs that are used by all users.
 700  | `rwx------` | The file's owner may read, write, and execute the file. Nobody else has any rights. This setting is useful for programs that only the owner may use and must be kept private from others.
 666  | `rw-rw-rw-` | All users may read and write the file.
 644  | `rw-r--r--` | The owner may read and write a file, while all others may only read the file. A common setting for data files that everybody may read, but only the owner may change.
 600  | `rw-------` | The owner may read and write a file. All others have no rights. A common setting for data files that the owner wants to keep private (including SSH keys).

**Here are some useful settings for directories:**

Value | Meaning     | Description
:---: | ----------- | ----------------------------------------
 777  | `rwxrwxrwx` | No restrictions on permissions. Anybody may list, create, and delete files in the directory. Generally, this is not a secure setting.
 755  | `rwxr-xr-x` | The directory owner has full access. All others may list the directory, but cannot create files nor delete them. This setting is common for directories that you wish to share with other users.
 700  | `rwx------` | The directory owner has full access. Nobody else has any rights. This setting is useful for directories that only the owner may use and must be kept private from others.
