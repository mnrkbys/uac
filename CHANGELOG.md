# Changelog

## 3.0.0 (2024-10-22)

### Features

- New '--enable-modifiers' command line option. Enabling this option will case UAC to run artifacts that change the current system state ([#272](https://github.com/tclahr/uac/issues/272)).
- UAC now completely skips an artifact file (YAML) that has no artifacts to be collected for the target operating system. You can use '--artifacts list [OPERATING_SYSTEM]' to display artifacts for a specific operating system only.
- New output file formats:
  - none: Collected data will not be archived or compressed. Instead, it will be copied directly to an output directory ([#188](https://github.com/tclahr/uac/issues/188)).
  - zip: Collected data will be archived and compressed into a zip file. Additionally, you can create a password-protected zip file using the '--output-password' option ([#149](https://github.com/tclahr/uac/issues/149)).
- You can now set a custom output file name using the '-o/--output-base-name' command line option. Variables are available to format the filename ([#179](https://github.com/tclahr/uac/issues/179)).
- Now you have the option to supply a file path to a custom profile located outside the profiles directory.
- Now you have the option to supply a file path to a custom artifact located outside the artifacts directory ([#154](https://github.com/tclahr/uac/issues/154)).
- Now you can have the option to supply a file path to a custom config file located outside the config directory using the '-c/--config' command line option.
- New remote transfer options for Amazon, Google and IBM cloud storage locations.
- UAC will now use 'wget' to transfer files to remote cloud storage locations when 'curl' is not available.
- You can now increase the verbosity level using the '-v/--verbose' command line option. Enabling a higher verbosity level will result in the display of all executed commands.
- UAC will now use the built-in function 'astrings' to extract strings from binary files when 'strings' is not available on the system.
- The message 'The strings command requires the command line developer tools.' will no longer appear on macOS systems without developer tools installed ([#171](https://github.com/tclahr/uac/issues/171)).
- Error messages generated by executed commands (stderr) are now recorded in the uac.log file ([#150](https://github.com/tclahr/uac/issues/150)).
- New '-H/--hash-collected' command line option. Enabling this option will cause UAC to hash all collected files and save the results in a hash file. To accomplish this, all collected data must first be copied to the destination directory. Therefore, ensure you have twice the free space available on the system: once for the collected data and once for the output file. Additionally, note that this process will increase the running time ([#189](https://github.com/tclahr/uac/issues/189)).
- You can now validate profiles using the '--validate-profile' command line option.

### Artifacts

- bodyfile/bodyfile.yaml: Updated to remove max_depth limit.
- files/applications/git.yaml: Added collection of files that can be used to run persistence [linux, macos] ([mnrkbys](https://github.com/mnrkbys)).
- files/applications/lesshst.yaml: Added less history file (.lesshst) collection [aix, freebsd, linux, macos, netbsd, netscaler, openbsd, solaris] ([mnrkbys](https://github.com/mnrkbys)).
- files/applications/whatsapp.yaml: Added collection of WhatsApp Desktop files [macos].
- files/logs/additional_logs.yaml: Artifact was renamed to advanced_log_search.yaml.
- files/logs/relink.yaml: Added collection of the kernel relink log file [openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/logs/run_log.yaml: Added collection of /run/log directory.
- files/packages/apt.yaml: Add artifacts to collect package manager plugins/scripts [linux] ([mnrkbys](https://github.com/mnrkbys)).
- files/packages/dnf.yaml: Add artifacts to collect package manager plugins/scripts [linux] ([mnrkbys](https://github.com/mnrkbys)).
- files/packages/pkg_contents.yaml: Updated to collect FreeBSD installed packages database [freebsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/packages/yum.yaml: Add artifacts to collect package manager plugins/scripts [linux] ([mnrkbys](https://github.com/mnrkbys)).
- files/system/acct.yaml: Added collection of system accounting files [freebsd, netbsd, openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/system/acct.yaml: Updated to collect system accounting files [solaris] ([sec-hbaer](https://github.com/sec-hbaer)).
- files/system/dev_db.yaml: Added collection of the database file used for device lookups [netbsd, openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/system/dev_shm.yaml: Updated to increase max_file_size to 10MB.
- files/system/locate_db.yaml: Added collection of the database file used by locate command, representing a snapshot of the virtual file system accessible with minimal permissions [freebsd, netbsd, openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/system/netscaler.yaml: Updated to increase max_file_size to 10MB.
- files/system/run_shm.yaml: Updated to increase max_file_size to 10MB.
- files/system/security_backups.yaml: Added collection of file backups and hashes created by the integrated security script [freebsd, netbsd, openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- files/system/systemd.yaml: Updated to add new locations for configuration files.
- files/system/tmp.yaml: Updated to increase max_file_size to 10MB.
- files/system/udev.yaml: Added collection of udev rule files ([mnrkbys](https://github.com/mnrkbys)).
- files/system/var_tmp.yaml: Updated to increase max_file_size to 10MB.
- hash_executables/hash_executables.yaml: Updated to remove max_depth and max_file_size properties.
- live_response/containers/jls.yaml: Added collection of jails used on FreeBSD systems [freebsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- live_response/hardware/dmesg.yaml: Updated collection of console message bufffer [esxi, freebsd, netscaler, openbsd, solaris] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- live_response/modifiers/revel_hidden_processes.yaml: Added command to umount filesystems mounted onto a directory that tipically corresponds to a process ID (PID) [linux] ([halpomeranz](https://github.com/halpomeranz)).
- live_response/network/procfs_information.yaml: Added collection of TCP and UDP network details from /proc/net [linux]. 
- live_response/process/deleted.yaml: Collection of deleted processes will no longer use dd conv=swab. The binary file will be collected in its raw format now [linux].
- live_response/process/deleted.yaml: Updated to fix the collection of open files of (malicious) processes [linux] ([mnrkbys](https://github.com/mnrkbys)).
- live_response/process/hash_running_processes.yaml: Updated to add support to hash running processes on FreeBSD systems that are using procfs (/proc) [freebsd].
- live_response/process/procfs_information.yaml: Added artifact collection using cat when strings is not available.
- live_response/process/procfs_information.yaml: Updated to collect /proc/*/mount [linux] ([halpomeranz](https://github.com/halpomeranz)).
- live_response/process/procfs_information.yaml: Updated to collect /proc/*/stat [linux] ([mnrkbys](https://github.com/mnrkbys)).
- live_response/process/strings_running_processes.yaml: Added collection of strings from running processes for ESXi systems [esxi].
- live_response/process/strings_running_processes.yaml: Added condition to check whether developer tools are installed before running strings on macOS [macos].
- live_response/process/strings_running_processes.yaml: Added support for collecting strings even when the strings command is unavailable. In such cases, the built-in astrings command will be used instead [all].
- live_response/storage/btrfs.yaml: Added collection of btrfs mountpoints, subvolumes and snapshots information [linux] ([mnrkbys](https://github.com/mnrkbys)).
- live_response/system/acctadm.yaml: Added collection of configuration for extended accounting [solaris] ([sec-hbaer](https://github.com/sec-hbaer)).
- live_response/system/acctcom.yaml: Added collection of the last commands executed in a reverse order based on the default and historic accounting files [solaris] ([sec-hbaer](https://github.com/sec-hbaer)).
- live_response/system/bpftool.yaml: Added eBPF programs information collection using bpftool [linux] ([mnrkbys](https://github.com/mnrkbys)).
- live_response/system/hidden_directories.yaml: Updated to remove max_depth limit.
- live_response/system/hidden_files.yaml: Updated to remove max_depth limit.
- live_response/system/kernel_tainted_state.yaml: Added collection of dmesg messages showing modules tainting the kernel [linux].
- live_response/system/lastcomm.yaml: Added collection of the last commands executed in a reverse order based on the default and historic accounting file [freebsd, netbsd, openbsd] ([Herbert-Karl](https://github.com/Herbert-Karl)).
- live_response/system/lastcomm.yaml: Updated to collect the last commands executed in a reverse order based on the extended accounting file [solaris] ([sec-hbaer](https://github.com/sec-hbaer)).
- live_response/system/sgid.yaml: Updated to remove max_depth limit.
- live_response/system/socket_files.yaml: Updated to remove max_depth limit.
- live_response/system/suid.yaml: Updated to remove max_depth limit.
- live_response/system/sys_modules.yaml: Removed as it is was duplicate artifact with kernel_modules.yaml.
- live_response/system/world_writable_directories.yaml: Updated to remove max_depth limit.
- live_response/system/world_writable_files.yaml: Updated to remove max_depth limit.
- live_response/system/zoneadm.yaml: Artifact was moved to live_response/containers directory ([Herbert-Karl](https://github.com/Herbert-Karl)).

### Profiles

- files/applications/git.yaml, files/applications/lesshst.yaml, files/applications/viminfo.yaml, and files/applications/wget.yaml artifacts were added to the 'ir_triage' profile.

### Command Line Option Changes

- '--date-range-start' was renamed to '--start-date' ([#186](https://github.com/tclahr/uac/issues/186)).
- '--date-range-end' was renamed to '--end-date' ([#186](https://github.com/tclahr/uac/issues/186)).
- '--validate-artifacts-file' was renamed to '--validate-artifact'.
- '--s3-presigned-url' was renamed to '--aws-s3-presigned-url'.
- '--s3-presigned-url-log-file' was renamed to '--aws-s3-presigned-url-log-file'.
- '--ibm-cos-url', '--ibm-cos-url-log-file' and '--ibm-cloud-api-key' were removed and now transfers to IBM cloud should be done using '--s3-provider', '--s3-region', '--s3-bucket' and '--s3-token' options.

### Artifacts Properties Changes

- Introduced a new global 'modifier' property that ensures the artifact runs only if '--enable-modifiers' command line option is used.
- Introduced a new 'condition' property that ensures the collection runs only if the specified condition returns true.
- The 'output_directory' property is now mandatory for the following collectors: command, find, hash and stat.
- The 'file_type' property is now an array.
- The 'permissions' property is now an array.

### uac.conf

- Introduced a new global 'max_depth' configuration option to limit the depth of directory tree searches globally.

### Tools

- Statically linked 'zip' is now available for the following systems:
  - linux/esxi (arm, arm64, i386 and x86_64)
  - freebsd/netscaler (i386 and x86_64)
- 'avml' and 'linux_procmemdump.sh' tools were moved to the 'bin' directory.
- AVML updated to v0.14.0.

### Deprecated

- Android support was removed, but UAC can still be executed on Android systems using '--operating-system linux' option.
