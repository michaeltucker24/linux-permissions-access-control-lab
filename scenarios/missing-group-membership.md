# Scenario 002: Missing Group Membership

## Reported Issue

A user reports that they cannot access a project directory even though the directory permissions appear to allow group access.

## Impact

The user cannot access shared project files required for their work.

## Environment

- OS: Ubuntu Linux
- Directory: `/shared/project`
- Group: `projectteam`
- Tools: `id`, `groups`, `usermod`, `newgrp`, `ls`

## Investigation Steps

### 1. Check directory ownership and permissions

```bash
ls -ld /shared/project
```

The directory is owned by group `projectteam`.

### 2. Check the user's group membership

```bash
id username
groups username
```

The user is not listed as a member of `projectteam`.

### 3. Add the user to the required group

```bash
sudo usermod -aG projectteam username
```

### 4. Apply group membership

The user may need to log out and back in. For immediate shell testing:

```bash
newgrp projectteam
```

### 5. Verify updated group membership

```bash
id username
groups username
```

### 6. Test access

```bash
su - username
touch /shared/project/testfile.txt
```

## Commands Used

```bash
ls -ld /shared/project
id username
groups username
sudo usermod -aG projectteam username
newgrp projectteam
su - username
touch /shared/project/testfile.txt
```

## Root Cause

The directory permissions allowed access for the `projectteam` group, but the affected user was not a member of that group.

## Resolution

The user was added to the required group.

```bash
sudo usermod -aG projectteam username
```

## Verification

After the group membership was applied, the user was able to create a test file in the shared directory.

## Customer-Facing Update

The access issue was resolved. The shared directory was configured for group access, but the user was missing the required group membership. The user was added to the group and access was verified.

## Lessons Learned

Group-based permissions require both correct directory permissions and correct user group membership. Users may need to start a new login session before updated group membership takes effect.
