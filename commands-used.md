# Commands Used

This file lists the primary commands used throughout the Linux Permissions and Access Control Lab.

## Confirm user identity and groups

```bash
id username
groups username
```

## Check ownership and permissions

```bash
ls -l /path/to/file
ls -ld /path/to/directory
```

## Check parent directory permissions

```bash
namei -l /path/to/file
```

## Change file ownership

```bash
sudo chown user:group /path/to/file
sudo chown -R user:group /path/to/directory
```

## Change group ownership

```bash
sudo chgrp groupname /path/to/file
sudo chgrp -R groupname /path/to/directory
```

## Change permissions

```bash
sudo chmod 640 /path/to/file
sudo chmod 750 /path/to/directory
sudo chmod 2770 /shared/project
```

## Add user to a group

```bash
sudo usermod -aG groupname username
```

## Apply new group membership in current shell

```bash
newgrp groupname
```

## Review ACLs

```bash
getfacl /path/to/file
getfacl /path/to/directory
```

## Set ACL access

```bash
sudo setfacl -m u:username:rwx /path/to/directory
sudo setfacl -m g:groupname:rwx /path/to/directory
```

## Remove ACL entry

```bash
sudo setfacl -x u:username /path/to/directory
```

## Test access as another user

```bash
su - username
touch /shared/project/testfile.txt
cat /shared/project/project-file.txt
```
