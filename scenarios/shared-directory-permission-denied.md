# Scenario 001: Shared Directory Permission Denied

## Reported Issue

A user reports that they cannot create or modify files inside a shared project directory.

## Impact

The user cannot complete required work in the shared directory, which may delay team collaboration or application workflows.

## Environment

- OS: Ubuntu Linux
- Directory: `/shared/project`
- Tools: `ls`, `id`, `groups`, `chmod`, `chown`, `namei`

## Investigation Steps

### 1. Confirm affected user identity

```bash
id username
```

### 2. Check user group membership

```bash
groups username
```

### 3. Check shared directory permissions

```bash
ls -ld /shared/project
```

### 4. Check parent directory traversal permissions

```bash
namei -l /shared/project
```

### 5. Review ownership

```bash
ls -ld /shared
ls -ld /shared/project
```

### 6. Correct group ownership

```bash
sudo chown root:projectteam /shared/project
```

### 7. Correct shared directory permissions

```bash
sudo chmod 2770 /shared/project
```

### 8. Verify access as affected user

```bash
su - username
touch /shared/project/testfile.txt
```

## Commands Used

```bash
id username
groups username
ls -ld /shared/project
namei -l /shared/project
ls -ld /shared
sudo chown root:projectteam /shared/project
sudo chmod 2770 /shared/project
su - username
touch /shared/project/testfile.txt
```

## Root Cause

The shared directory did not have the correct group ownership and permission settings, preventing the user from writing to the directory.

## Resolution

The directory group ownership was corrected, and group read/write/execute permissions were applied. The setgid bit was also applied so new files inherit the project group.

```bash
sudo chown root:projectteam /shared/project
sudo chmod 2770 /shared/project
```

## Verification

The affected user was able to create a test file inside the shared directory.

```bash
touch /shared/project/testfile.txt
```

## Customer-Facing Update

The shared directory access issue was resolved. The directory ownership and permissions were corrected, and write access was successfully verified.

## Lessons Learned

Shared directory access issues often involve both ownership and permission bits. The setgid bit can help maintain consistent group ownership for new files created in shared directories.
