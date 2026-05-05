# Linux Permissions and Access Control Lab

## Overview

This repository documents Linux permissions troubleshooting scenarios focused on file ownership, group access, permission bits, ACLs, and shared directory access issues.

The purpose of this project is to practice resolving common “permission denied” issues in Ubuntu/Linux support environments.

## Scenario

A user reports that they cannot read, write, or modify files inside a shared project directory. The issue may involve incorrect ownership, missing group membership, restrictive permissions, ACL configuration, or parent directory access.

## Objectives

- Identify the affected user
- Confirm group membership
- Review file and directory ownership
- Inspect permission bits
- Check parent directory permissions
- Review ACLs
- Apply the correct access fix
- Verify user access
- Document the root cause and resolution

## Environment

- OS: Ubuntu Linux
- Shell: Bash
- Tools: `id`, `groups`, `ls`, `chmod`, `chown`, `chgrp`, `getfacl`, `setfacl`, `namei`, `su`

## Skills Demonstrated

- Linux user and group troubleshooting
- File ownership analysis
- Permission bit review
- ACL investigation
- Shared directory access troubleshooting
- Root cause analysis
- Technical documentation
- Customer-facing technical updates

## Scenario Index

| Scenario | Issue | Key Tools | Link |
|---|---|---|---|
| Scenario 001 | Shared directory permission denied | `ls`, `id`, `groups`, `chmod`, `chown` | [View Scenario](scenarios/shared-directory-permission-denied.md) |
| Scenario 002 | Missing group membership | `id`, `groups`, `usermod`, `newgrp` | [View Scenario](scenarios/missing-group-membership.md) |
| Scenario 003 | ACL access issue | `getfacl`, `setfacl`, `namei` | [View Scenario](scenarios/acl-access-issue.md) |

## Investigation Workflow

### 1. Confirm user identity and groups

```bash
id username
groups username
```

### 2. Check file and directory permissions

```bash
ls -l /shared/project-file.txt
ls -ld /shared
ls -ld /shared/project
```

### 3. Check parent directory permissions

```bash
namei -l /shared/project/project-file.txt
```

### 4. Review ACLs

```bash
getfacl /shared/project
```

### 5. Apply ownership or group correction

```bash
sudo chown root:projectteam /shared/project
sudo chmod 2770 /shared/project
```

### 6. Add user to required group

```bash
sudo usermod -aG projectteam username
```

### 7. Optional ACL correction

```bash
sudo setfacl -m u:username:rwx /shared/project
```

## Common Root Causes

- User is not a member of the required group
- File or directory has incorrect owner
- Group ownership is incorrect
- Permissions are too restrictive
- Parent directory does not allow traversal
- ACLs override or restrict access
- User has not logged out/in after group membership change

## Verification Checklist

Before closing a permissions-related support ticket, verify:

- User identity and group membership are correct
- Ownership is correct
- Permission bits match the intended access
- Parent directories allow traversal
- ACLs are reviewed where applicable
- User can read/write as expected
- Access test is performed as the affected user
- Findings and resolution are documented clearly

## Customer-Facing Update Example

The shared directory access issue was resolved. The user was missing the required group membership, so the system denied access to the project directory. Group membership was corrected and access was verified successfully.

## Lessons Learned

Linux access issues should be checked across multiple layers: user identity, group membership, ownership, permission bits, ACLs, and parent directory permissions.

## Portfolio Note

This project is part of my Linux Support Engineer portfolio. It demonstrates practical troubleshooting, documentation, and systems administration skills relevant to Ubuntu/Linux support roles.
