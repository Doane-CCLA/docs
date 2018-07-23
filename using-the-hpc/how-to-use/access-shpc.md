[CADES](http://support.cades.ornl.gov/) → [User Documentation](../../README.md) → [SHPC Condo User Guide](../overview.md) → [How to Use](how-to-use.md) → [Access Your Allocation](access-shpc.md)

# Access Your SHPC Condo Allocation

After your [access request](request-access.md) has been approved and you have installed the [prerequisites](prerequisites.md), you can log in to the Open Protection Zone or the Moderate Protection Zone.

## Open Protection Zone

1. Open a Bash terminal (or see [here](prerequisites.md) if you need more help).

2. Execute `ssh username@or-condo-login.ornl.gov`. Replace `username` with your _UCAMS/XCAMS ID_.

3. When prompted, enter your password.

## Moderate Protection Zone

1. Open a Bash terminal (or see [here](prerequisites.md) if you need more help).

2. Execute `ssh username@mod-condo-login.ornl.gov`. Replace `username` with your _UCAMS/XCAMS ID_.

3. When prompted, enter your password.

**By default, `/home` directories should be automatically created for you when logging into SHPC Condos**.

You can run the following command on your terminal to see your files:

```bash
# ls -lhtr /home/username
total 20K
drwxr-xr-x 2 username users 4 Apr 6 12:11 Test1
-rw-r--r-- 1 username users 982 Apr 6 12:11 setup.py
-rw-r--r-- 1 username users 1.5K Apr 6 12:11 readme.txt
-rw-r--r-- 1 username users 77 Apr 6 12:11 paralleltestpy2.py
```

📝 Replace the word `username` with your **UCAMS/XCAMS ID**.

- The `ls -lhtr /home/username` command will show the whole list and details of the files that the **username** has.
