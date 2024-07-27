
## Task 1: Secure Web Application Deployment with Firewalld, httpd, and SELinux

You have a web application running on a non-standard port (e.g., 8081) with content served from a custom directory (e.g., `/opt/myapp`). Your goal is to make the application accessible to external users while ensuring the system's security. To achieve this, you need to:

1. **Configure firewalld** to allow inbound traffic on the specific port used by your web application.
2. **Ensure httpd** is configured correctly to serve content from the custom directory.
3. **Adjust SELinux settings** to permit httpd to listen on the non-standard port and access the custom directory.

## Task 2: Advanced User and Group Management

Create the following users, groups, and group memberships, adhering to specific requirements:

1. **Group**: A group named `developers` with a Group ID (GID) of 1025.
2. **User**: A user named `alice` who belongs to the `developers` group as their primary group.
3. **User**: A user named `bob` who belongs to the `developers` group as a secondary group.
4. **User**: A user named `eve` who does not have a home directory and is restricted from logging in interactively.
5. **Password**: All users (`alice`, `bob`, and `eve`) should have the same initial password, but this password must expire immediately upon their first login, requiring them to set a new password.

## Task 3: Advanced Collaborative Directory with Custom umask

Create a collaborative directory `/shared/dev` with these specific attributes:

1. **Group Ownership**: The group `developers` should own the directory.
2. **Permissions**:
    - Members of the `developers` group should have read, write, and execute permissions.
    - Other users should have no permissions (neither read, write, nor execute).
    - The directory's setgid (SGID) bit should be set.
3. **File Creation**: Files created within `/shared/dev` should automatically have the following permissions:
    - Owner: Read and write permissions.
    - Group (developers): Read and write permissions.
    - Others: No permissions.

## Task 4: Advanced Autofs Configuration with Multiple NFS Shares and Timeout

Configure Autofs to achieve the following:

1. **Mount Points**: Automatically mount the following NFS shares from a remote server (e.g., `server2.example.com`) to specific locations on the local system:
    - `/projects` (NFS share: `/data/shared_projects`)
    - `/backups` (NFS share: `/data/server_backups`)
2. **Permissions and Options**:
    - The `/projects` mount should be accessible in read-write mode for all users.
    - The `/backups` mount should be accessible in read-only mode for all users.
    - Both mounts should have a specific timeout value (e.g., 300 seconds) after which they will be unmounted if not in use.
3. **Additional Requirements**:
    - Implement a custom error message that will be displayed to users if the remote NFS server is unavailable.
    - Ensure that the Autofs configuration persists after a system reboot.

**Additional Challenge**: Consider adding a third NFS share that is only accessible to members of a specific group (e.g., developers).

## Task 5: Advanced Cron Job with Script Execution and Logging

1. **Script**: Create a shell script named `/usr/local/bin/daily_backup.sh` that performs the following:
    - Creates a compressed archive (tar.gz) of the `/home/alice` directory.
    - Stores the backup archive in the `/var/backups` directory with a filename that includes the current date and time.
    - Logs any errors encountered during the backup process to a file named `/var/log/daily_backup.log`.
2. **Cron Job**: Schedule a cron job for the user `bob` to run the `/usr/local/bin/daily_backup.sh` script:
    - The job should run at 2:30 AM every Monday, Wednesday, and Friday.
    - The job's output (both standard output and standard error) should be emailed to the user `bob`.

Ensure that the cron job is configured correctly and that the backup script functions as expected.

## Task 6: Advanced ACL Permissions with Inheritance and Negation

Copy the file `/etc/fstab` to `/var/tmp`. Configure ACL permissions on `/var/tmp/fstab` with the following requirements:

1. **Ownership**:
    - The file should be owned by the root user.
    - The file should belong to the group `wheel`.
2. **Standard Permissions**:
    - The file should be readable and writable by the owner.
    - The file should be readable by the group `wheel`.
    - The file should be readable by all other users.
3. **ACL Permissions**:
    - The user `alice` should have read and write access.
    - The user `bob` should have read-only access.
    - The user `eve` should be explicitly denied any access (read, write, or execute).
4. **Inheritance**: Ensure that these ACL permissions are inherited by any new files or directories created within `/var/tmp/fstab`.

## Task 7: Advanced NTP Configuration with Multiple Servers and Monitoring

Configure your system to be an NTP client synchronized with multiple time servers:

1. **Time Servers**: Use a combination of public NTP servers (e.g., `pool.ntp.org`) and a private NTP server within your network (e.g., `ntp.example.com`).
2. **Fallback**: Implement a mechanism to automatically switch to a different time server if one becomes unavailable.
3. **Monitoring**: Set up monitoring to track the synchronization status of the NTP client and send alerts if there are any issues.
4. **Logging**: Configure NTP to log synchronization events and errors to a specific log file for later analysis.

## Task 8: Find and Archive Files by Multiple Criteria

Locate and archive files within the `/home` directory based on the following criteria:

1. **Size**: Files larger than 500 KB.
2. **Age**: Files that have not been modified in the last 90 days.
3. **Type**: Only files with the `.log` extension.

Copy these files to the `/archive/old_logs` directory, preserving their original directory structure. Ensure that the archived files are compressed (e.g., using gzip) to save space.

## Task 9: Advanced User Management and File Permissions

1. **User Creation with Specific UID**: Create a new user with the following attributes:
    - Username: `sarah`
    - UID: 1500
    - Password: A strong, randomly generated password (avoid using a fixed password like "password123")
    - Group: Assign the user to a specific group (e.g., `developers`) as their primary group.
2. **Incremental Backup with Hard Links**: Create a backup of the `/etc` directory:
    - Use the `/root/backups` directory as the backup location.
    - Name the backup file with the current date and time (e.g., `etc_backup_20240727.tar`).
    - Instead of creating a full copy of all files, use hard links to save disk space for files that have not changed since the previous backup.
    - Implement a mechanism to rotate old backups, keeping only a certain number of the most recent backups.
3. **Custom umask Configuration**: Configure a custom umask value for the user `bob`:
    - New files created by `bob` should have the following permissions: `-rw-r-----`
    - New directories created by `bob` should have the following permissions: `drwxr-x---`
    - Ensure that the custom umask persists across login sessions for the user `bob`.

## Task 10: Advanced Password Policies and Sudo Configuration

1. **Password Policy**: Implement a password policy on `server2.example.com` with the following requirements:
    - Expiration: Passwords for all users must expire after 60 days.
    - History: Users cannot reuse any of their last 5 passwords.
    - Warning: Users should receive a warning message 14 days before their password expires.
    - Inactive Accounts: Accounts that have been inactive for 90 days should be automatically locked.
2. **Sudo Configuration**:
    - Group Privileges: Grant sudo privileges to the `developers` group, allowing members to run any command without a password.
    - Logging: Configure sudo to log all commands executed by members of the `developers` group to a separate log file (e.g., `/var/log/sudo_developers.log`).
    - Restrictions: Prevent members of the `developers` group from running specific commands as root (e.g., `rm`, `shutdown`, `reboot`) through sudo.

Ensure that the password policy and sudo configuration are applied correctly and that you can verify their functionality.

## Task 11: Advanced Bash Shell Script for File Management
Create a bash script named `cleanup_logs.sh` located in `/usr/local/bin` that does the following:
1. **Log File Search**: Find all log files (with the `.log` extension) under `/var/log` that are older than 30 days.
2. **Compression**: Compress each found log file into a `.gz` archive, using a filename that includes the original filename and the current date (e.g., `access_log.20240727.gz`).
3. **Archiving**: Move the compressed log archives to a dedicated directory (e.g., `/var/log/archive`).
4. **Logging**: Maintain a log file (`/var/log/cleanup_logs.log`) that records the script's actions, including the files processed, compression results, and any errors encountered.
   - **Additional Challenge**: Implement an option in the script to allow specifying the number of days to retain log files before archiving/compressing.

## Task 12: Advanced Partitioning and LVM Configuration with Custom Physical Extent Size
1. **Swap Partition**: Create a swap partition with a size of 2 GB and label it as `swap_partition`.
2. **LVM Setup**:
   - Create a new physical volume (PV) on an existing disk or partition (e.g., `/dev/sdb1`).
   - Set the physical extent size (PE size) of the PV to 8 MB (instead of the default 4 MB).
   - Create a volume group (VG) named `appdata` and add the newly created PV to it.
   - Create two logical volumes (LVs) within the `appdata` VG:
     - `lv_app1` with a size of 500 MB and ext4 filesystem, mounted at `/opt/app1`.
     - `lv_app2` with a size of 1 GB and xfs filesystem, mounted at `/opt/app2`.
   - **Additional Challenge**: Implement a mechanism to automatically extend the `lv_app2` logical volume if its usage exceeds 80%.

## Task 13: Advanced LVM Thin Provisioning with Multiple Thin Volumes and Snapshot
1. **Physical Volume and Volume Group**:
   - Create a new physical volume (PV) on the device `/dev/sdc`.
   - Create a volume group (VG) named `thin_vg` using this new PV.
2. **Thin Pool and Thin Volumes**:
   - Create a thin pool logical volume (LV) named `thinpool` within the `thin_vg` VG, with a size of 100GB.
   - Create two thinly provisioned logical volumes from the `thinpool`:
     - `thin_lv1` with a virtual size of 50GB and ext4 filesystem, mounted at `/mnt/thin_lv1`.
     - `thin_lv2` with a virtual size of 75GB and xfs filesystem, mounted at `/mnt/thin_lv2`.
3. **Snapshot**:
   - Create a snapshot of the `thin_lv1` logical volume before making any changes to its data.

## Task 14: Resize Logical Volume and Underlying Filesystem
1. **Logical Volume Expansion**: Extend the logical volume mounted at `/mnt/thin_lv1` by an additional 20GB.
2. **Filesystem Resize**: Resize the underlying filesystem (ext4) on the `/mnt/thin_lv1` logical volume to match the new size.
3. **Verification**: Verify that the filesystem has been successfully resized and that the additional space is available for use.

## Task 15: Advanced Tuned Profile Configuration for Specific Workload
Identify and apply the most suitable tuned profile for a server that primarily runs a database application with heavy disk I/O and requires low latency. After setting the profile, verify that it has been applied correctly and monitor the system's performance metrics to ensure the desired improvements.

## Task 16: Advanced Container Setup with Custom User, Network, and Restart Policy
1. **Container Creation**: Create a container named `myapp` using a specified image from a private registry (e.g., your company's registry). The container should run as a non-root user named `appuser`.
2. **Network Configuration**:
   - Connect the container to a user-defined bridge network (e.g., `myapp_network`).
   - Assign a static IP address to the container within the network.
   - Expose specific ports on the container to the host system.
3. **Systemd Service**:
   - Create a systemd service unit file to manage the container.
   - Configure the service to start automatically on boot and restart on failure, using a specific restart policy (e.g., `on-failure`).
   - Ensure proper logging of the container's output to a designated log file.

## Task 17: Container Storage and Logging Configuration with SELinux Considerations
1. **Persistent Storage**: Configure the `myapp` container to use a named volume (e.g., `myapp_data`) for persistent storage of application data. The volume should be mounted to a specific directory within the container.
2. **Log Collection**:
   - Configure the container to log application logs to a file within the `/var/log/myapp` directory on the host system.
   - Use a log rotation mechanism to manage log file size and prevent them from consuming excessive disk space.
3. **SELinux**:
   - Ensure that SELinux is configured to allow the container to access the mounted volume and log files.
   - Label the named volume and log files appropriately to match the container's SELinux context.
   - Consider using SELinux booleans or custom policies to fine-tune access controls if needed.

## Task 18: Advanced SSH Hardening and Security Auditing
1. **SSH Configuration**:
   - Disable direct root login via SSH.
   - Change the default SSH port to a non-standard, high-numbered port.
   - Enforce key-based authentication for all users, including root, and disable password authentication.
   - Limit SSH access to specific IP addresses or subnets.
2. **Auditd Configuration**:
   - Configure `auditd` to log successful and failed SSH login attempts, including the source IP address and username.
   - Monitor file access events for sensitive files and directories (e.g., `/etc/shadow`, `/etc/passwd`).
   - Track changes to user and group accounts, including password modifications and privilege escalations.
   - Implement real-time alerting for critical security events detected by `auditd`.
3. **SELinux Policy Customization**:
   - Create a custom SELinux policy module to allow a specific web server (e.g., Nginx) to access files in a non-standard directory (e.g., `/opt/webdata`).
   - Test the custom policy module in permissive mode to identify any potential issues before enforcing it.
   - Document the changes made to the SELinux policy for future reference and troubleshooting.

## Task 19: Advanced System Monitoring with Bash Script, Journalctl, and Logrotate
1. **Bash Script for System Monitoring**:
   - Develop a Bash script (`/usr/local/bin/monitor_system.sh`) that checks system metrics (CPU usage, memory usage, disk space) at regular intervals and logs the results. Include error handling and a mechanism to notify administrators (e.g., via email) if critical thresholds are exceeded.
2. **Journalctl Log Analysis**:
   - Use `journalctl` with appropriate filters (e.g., by unit, time range, priority) to investigate a specific system issue. For example, analyze logs related to a failed service start or a sudden increase in resource usage.
   - Aggregate and summarize log data using `journalctl` options to identify patterns or trends in system behavior.
3. **Logrotate Configuration**:
   - Create a `logrotate` configuration file (`/etc/logrotate.d/monitor_system`) tailored to the `monitor_system.log` file generated by the Bash script.
   - Configure `logrotate` to:
     - Rotate the log file weekly.
     - Keep 4 weeks' worth of log files.
     - Compress rotated log files using a specific compression algorithm (e.g., `bzip2`).
     - Run a post-rotation script to perform additional actions (e.g., send a notification email with a summary of log events).
4. **Persistent Journal**:
   - Increase the storage capacity for persistent journal logs.
   - Implement a strategy to automatically archive or purge older journal logs to prevent them from consuming excessive disk space.
   - Verify the integrity of the persistent journal after a system reboot and troubleshoot any potential issues.
