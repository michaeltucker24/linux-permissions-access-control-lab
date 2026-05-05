# Scenario 003: ACL Access Issue

## Reported Issue

A user reports that they cannot access a directory even though standard Linux permissions appear correct.

## Impact

The user cannot access required files, and the issue is not obvious from standard `ls -l` output.

## Environment

- OS: Ubuntu Linux
- Directory: `/shared/project`
- Tools: `ls`, `getfacl`, `setfacl`, `namei`

## Investigation Steps

### 1. Check standard permissions

```bash
ls -ld /shared/project
```

Standard permissions appear correct.

### 2. Check parent directory permissions

```bash
namei -l /shared/project
```

Parent directory traversal appears correct.

### 3. Review ACL entries

```bash
getfacl /shared/project
```

An ACL entry is restricting or overriding expected access.

### 4. Correct the ACL

```bash
sudo setfacl -m u:username:rwx /shared/project
```

or for group access:

```bash
sudo setfacl -m g:projectteam:rwx /shared/project
```

### 5. Verify ACL

```bash
getfacl /shared/project
```

### 6. Test access

```bash
su - username
touch /shared/project/testfile.txt
```

## Commands Used

```bash
ls -ld /shared/project
namei -l /shared/project
getfacl /shared/project
sudo setfacl -m u:username:rwx /shared/project
sudo setfacl -m g:projectteam:rwx /shared/project
su - username
touch /shared/project/testfile.txt
```

## Root Cause

An ACL entry affected the user's access even though the standard ownership and permission bits looked correct.

## Resolution

The ACL was reviewed and corrected to allow the intended user or group access.

## Verification

Access was tested as the affected user, and file creation succeeded.

## Customer-Facing Update

The directory access issue was resolved. Standard permissions appeared correct, but an ACL entry was affecting access. The ACL was corrected and access was verified.

## Lessons Learned

When standard Linux permissions appear correct but access still fails, check ACLs with `getfacl`. ACLs can grant or restrict access beyond what is visible with basic `ls -l` output.
