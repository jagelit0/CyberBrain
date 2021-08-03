# Mounting VHD images.
```bash
# dependencies 'sudo apt-get install libguestfs-tools'

$ guestmount --add yourVirtualDisk.vhdx --inspector --ro /mnt/anydirectory
```