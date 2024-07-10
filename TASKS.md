# RHCSA Practice Exam Tasks

## Task 1: Configure the Network
1. Assign hostname and IP addresses for your virtual machines as per the following details:
   - Hostname: `server1.example.com`
   - IP Address: `192.168.14.151`
   - Netmask: `255.255.255.0`
   - Gateway: `192.168.14.1`
   - Name Server: `8.8.8.8`
   - Hostname: `server2.example.com`
   - IP Address: `192.168.14.132`
   - Netmask: `255.255.255.0`
   - Gateway: `192.168.14.1`
   - Name Server: `8.8.8.8`

## Task 2: Configure the Repositories
2. Configure the repositories which are available on the repo server at:
   - `http://repo.example.com/BaseOS`
   - `http://repo.example.com/AppStream`

## Task 3: Configure SELinux
3. Your web content has been configured on port `8080` at the `/var/www/html` directory (Don't alter or remove any files in this directory). Make the content accessible.

## Task 4: User and Group Management
4. Create the following users, groups, and group memberships:
   - (a) A group named `sysadmin`.
   - (b) A user `john` who belongs to `sysadmin` as a secondary group.
   - (c) A user `jane` who belongs to `sysadmin` as a secondary group.
   - (d) A user `doe` who does not have access to an interactive shell on the system and who is not a member of `sysadmin`.
   - (e) The users `john`, `jane`, and `doe` should all have the password `password123`.

## Task 5: Create a Collaborative Directory
5. Create a collaborative directory `/shared/sysadmin` with the following characteristics:
   - (a) Group ownership of `/shared/sysadmin` is `sysadmin`.
   - (b) The directory should be readable, writable, and accessible to members of `sysadmin`, but not any other user. (It is understood that root has access to all files and directories on the system.)
   - (c) Files created in `/shared/sysadmin` automatically have group ownership set to the `sysadmin` group.

## Task 6: Configure Autofs
6. Configure Autofs:
   - (a) To automatically mount the below NFS shares on `server1.example.com` machine at `/mnt/auto` directory:
     - `192.168.14.132:/export/public`
     - `192.168.14.151:/export/private`
   - (b) The public NFS share should have read-only access for all users.
   - (c) The private NFS share should have read-write access for all users.
   - (d) Both shares should get automatically unmounted if not in use for 60 seconds.

## Task 7: Set a Cron Job
7. (a) Set a Cron job for user `alex` to run at 3:15 AM every day that prints "Good morning" using the `echo` command.

## Task 8: Configure ACL Permissions
8. Configure the ACL permissions:
   - Copy the file `/etc/hosts` to `/var/tmp`. Configure the permission of `/var/tmp/hosts` so that:
     - (a) The file `/var/tmp/hosts` is owned by the `root` user.
     - (b) The file `/var/tmp/hosts` belongs to the group `root`.
     - (c) The file `/var/tmp/hosts` should not be executable by anyone.
     - (d) The user `john` is able to read and write to `/var/tmp/hosts`.
     - (e) The user `jane` can neither read nor write to `/var/tmp/hosts`.
     - (f) All other users (current/future) have the ability to read `/var/tmp/hosts`.

## Task 9: Configure NTP
9. Configure your system so that it is an NTP client of `server1.example.com` (192.168.14.151).

## Task 10: Locate & Copy Files
10. Find all files greater than 2 MB in the `/var` directory and copy them to the `/archive/largefiles` directory.

## Task 11: User Management and File Permissions
11. (a) Create a new user with UID 1400, username, and password as `david`.
    - (b) Create an archive file:
      - Backup `/home` as `/root/home_backup.tar.gz`.
    - (c) Set the permissions:
      - (i) All newly created files for user `natasha` should have `-rw-------` as the default permission.
      - (ii) All newly created directories for user `natasha` should have `drwx------` as the default permission.

## Task 12: Password Expiration and Sudo Privileges
12. (a) The password for all new users on `server2.example.com` should expire after 30 days.
    - (b) Assign the sudo privilege:
      - (a) Assign the sudo privilege for the group `sysadmin` so that group members can administrate without any password.

## Task 13: Create a Bash Shell Script Program
13. (a) Create a `findsmall` script to locate files under `/var/log` having size less than 500K.
    - (b) After executing the `findsmall` script, the listed (searched) files should be copied to `/root/logfiles`.

## Task 14: Create and Configure Partitions
14. (a) Create a swap partition of 1GB size.
    - (b) Create one logical volume named `webdata` on the `webstore` volume group with a size of 100 extents and assign the filesystem as `xfs`. The `webstore` volume group extents should be 4 MiB. Mount the logical volume under the mount point `/mnt/webdata`.

## Task 15: Set Up Logical Volume Using Thin Provisioning
15. (a) Create a new physical volume on the device `/dev/sdb`.
    - (b) Create a volume group named `vg_storage` using this physical volume.
    - (c) Create a thin pool logical volume named `pool_lv` with a size of 60G.
    - (d) Create a thinly provisioned logical volume named `thinvol` from `pool_lv` with a virtual size of 120G.
    - (e) Format the thinly provisioned logical volume with the `xfs` filesystem.
    - (f) Mount the logical volume to `/mnt/thinvol`.
    - (g) Ensure the logical volume is mounted automatically at boot.

## Task 16: Resize Logical Volume
16. Resize the logical volume size by adding 200 extents on `/mnt/webdata` directory.

## Task 17: Set the Recommended Tuned Profile
17. Set the recommended tuned profile for a server optimized for throughput.

## Task 18: Create and Configure a Container as a System Startup Service
18. (a) Create a container named `webserver` with the image `nginx` stored in Docker for the user `developer`.
    - (b) The container should be configured as a system startup service.
    - (c) The container directory `container_data` should be created for the `developer` user.

## Task 19: Configure Persistent Storage and Logging for the Container
19. (a) Configure the container with persistent storage that mounts `/var/log/nginx` to `/home/developer/container_logs`.
    - (b) The container directory contains all log files from `/var/log/nginx`.

## Task 20: Reset the Forgotten Root Password
20. Reset the forgotten root password on `server2.example.com` machine and set it to `redhat123`.
