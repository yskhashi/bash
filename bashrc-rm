alias rm='fn_rm_failsafe'

#
# == rm_blocklist == 
#
# A string "true" (case-insensitive) with exist is valid.
#

declare -A rm_blocklist=(
  [/]="true"
  [/bin]="true"
  [/boot]="true"
  [/boot/efi]="true"
  [/boot/grub2]="true"
  [/boot/loader]="true"
  [/dev]="true"
  [/dev/snd]="true"
  [/dev/vfio]="true"
  [/dev/net]="true"
  [/dev/mqueue]="true"
  [/dev/hugepages]="true"
  [/dev/rhel]="true"
  [/dev/disk]="true"
  [/dev/block]="true"
  [/dev/dri]="true"
  [/dev/bsg]="true"
  [/dev/virtio-ports]="true"
  [/dev/char]="true"
  [/dev/mapper]="true"
  [/dev/pts]="true"
  [/dev/shm]="true"
  [/dev/input]="true"
  [/dev/bus]="true"
  [/dev/raw]="true"
  [/dev/cpu]="true"
  [/lib]="true"
  [/lib64]="true"
  [/proc]="true"
  [/proc/fs]="true"
  [/proc/bus]="true"
  [/proc/irq]="true"
  [/proc/sys]="true"
  [/proc/tty]="true"
  [/proc/acpi]="true"
  [/proc/scsi]="true"
  [/proc/driver]="true"
  [/proc/sysvipc]="true"
  [/sbin]="true"
  [/sys]="true"
  [/sys/kernel]="true"
  [/sys/power]="true"
  [/sys/class]="true"
  [/sys/devices]="true"
  [/sys/dev]="true"
  [/sys/hypervisor]="true"
  [/sys/fs]="true"
  [/sys/fs/cgroup]="true"
  [/sys/bus]="true"
  [/sys/firmware]="true"
  [/sys/block]="true"
  [/sys/module]="true"
  [/etc]="true"
  [/root]="true"
  [/var]="true"
  [/var/lib]="true"
  [/var/log]="true"
  [/var/cache]="true"
  [/var/adm]="true"
  [/var/db]="true"
  [/var/empty]="true"
  [/var/ftp]="true"
  [/var/gopher]="true"
  [/var/local]="true"
  [/var/nis]="true"
  [/var/opt]="true"
  [/var/preserve]="true"
  [/var/spool]="true"
  [/var/tmp]="true"
  [/var/yp]="true"
  [/var/kerberos]="true"
  [/var/crash]="true"
  [/var/account]="true"
  [/var/snap]="true"
  [/var/cpq]="true"
  [/usr]="true"
  [/usr/bin]="true"
  [/usr/sbin]="true"
  [/usr/lib]="true"
  [/usr/lib64]="true"
  [/usr/share]="true"
  [/usr/include]="true"
  [/usr/libexec]="true"
  [/usr/local]="true"
  [/usr/src]="true"
  [/usr/config]="true"
  [/home]="true"
  [/media]="true"
  [/mnt]="true"
  [/opt]="true"
  [/srv]="true"
  [/tmp]="true"
)

fn_rm_failsafe()
{ 

  #
  # Convert the given path to an absolute path, then compare it againt a block_list.
  # If a match is found, terminate the function immediately.
  #

  if [[ $# -gt 0 ]]
  then

    declare -a argument=("$@")
    declare -a canonicalized_path
    mapfile -t canonicalized_path < <(realpath -sm -- "${argument[@]}")
    declare eval_path
    declare -i arg_count=0

    for eval_path in "${canonicalized_path[@]}"
    do
      : echo DEBUG: rm_blocklist["${eval_path}"] is \""${rm_blocklist[${eval_path}]}"\"
      if [[ "${rm_blocklist[${eval_path}]}" == [tT][rR][uU][eE] ]]
      then
        echo ERROR: \"rm\" bash alias has blocked the command execution.
        echo ERROR: the argument path \""${argument[${arg_count}]}"\" is in the \"rm_blocklist\". terminating.
        return 200
      else
        : echo DEBUG: rm_blocklist["${eval_path}"] is not true nor exist.
      fi
      ((arg_count++))
    done
  fi

  #
  # If no issues are found, execute the specified command below.
  #

  : echo DEBUG: execute command rm "$@"
  command rm "$@"
}
