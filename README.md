# File Permissions in Linux

## Project Description

The research team at the organization needed to update the file permissions for certain files and directories within the `projects` directory. The permissions did not currently reflect the level of authorization that should be given. Checking and updating these permissions helped keep the system secure. To complete this task, I performed the following steps:

---

## Checking File and Directory Details

I used the following command to determine the existing permissions set for the projects directory in the file system:

```bash
ls -la 
```

![image](https://github.com/user-attachments/assets/53ffe421-77fe-4657-8bf3-21195a09b955)

This command lists all contents of the `projects` directory, including hidden files, and provides detailed information on their permissions. The output indicated the presence of:
- One directory: `drafts`
- One hidden file: `.project_x.txt`
- Four other project files

Each file or directory had a **10-character permission string** in the first column, which determines access levels.

---

## Understanding the Permissions String

The 10-character permission string consists of:

| Position | Meaning |
|----------|---------|
| **1st character** | Indicates file type: `d` (directory) or `-` (regular file) |
| **2nd-4th characters** | Read (`r`), write (`w`), and execute (`x`) permissions for the **user** |
| **5th-7th characters** | Read (`r`), write (`w`), and execute (`x`) permissions for the **group** |
| **8th-10th characters** | Read (`r`), write (`w`), and execute (`x`) permissions for **others** |

For example, if a file has the permissions:

```bash
-rw-rw-r--  1 user group 1234 Feb 26 10:00 project_t.txt
```

- The first character (`-`) indicates it's a **regular file**.
- `rw-` (user) → User has **read and write** permissions.
- `rw-` (group) → Group has **read and write** permissions.
- `r--` (others) → Others have **read-only** permissions.

---

## Changing File Permissions

### Removing Write Access for Others

The organization determined that **others** shouldn't have write access to any files. I identified that `project_k.txt` had incorrect permissions, so I updated them using:

```bash
chmod o-w project_k.txt
ls -la
```

![image](https://github.com/user-attachments/assets/4fa80bb1-35f9-42da-aef5-0c49b4a1558f)

The `chmod` command removes write (`w`) permissions for **others** on `project_k.txt`, ensuring restricted access.

---

### Modifying Hidden File Permissions

The team archived `project_x.txt` and wanted to **prevent write access** while allowing only **read access** for the group. The hidden file `.project_x.txt` was modified with:

```bash
chmod u-w, g-w, g+r .project_x.txt

```
![image](https://github.com/user-attachments/assets/9d107a90-26ad-4b6c-93b3-cd120359d323)

This ensures:
- **User** loses write permissions (`u-w`)
- **Group** loses write permissions (`g-w`)
- **Group** gains read permissions (`g+r`)

---

### Restricting Directory Access

The organization decided that **only `researcher2` should have execute permissions** on the `drafts` directory. I ensured this by:

```bash
chmod g-x drafts
ls -la 
```

![image](https://github.com/user-attachments/assets/d424450b-d447-4d0a-bed5-275df4ed1f99)

This removed execute (`x`) permissions from the **group**, allowing only `researcher2` to access the directory contents.

---

## Summary

By following these steps, I successfully updated file and directory permissions in the `projects` directory to match the organization's security policies:
1. **Checked current permissions** using `ls -la`
2. **Modified file permissions** with `chmod` to restrict unauthorized write access
3. **Adjusted directory permissions** to limit access to specific users

These changes enhanced system security and ensured appropriate access levels for different users and groups.





