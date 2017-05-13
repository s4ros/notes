# Install Ubuntu alongside Windows10 - UEFI

- check if BIOS(?) is set to **UEFI-only** boot! Very important! No legacy shit.
- make some room for Ubuntu on the disk
- prepare bootable USB with **GPT** partition table + **boot** flag! Very important!
- you can create bootable USB from any bootable ISO image by:

```
sudo mkdir -p /mnt/{loop, mnt1}
sudo mount -o loop /opt/iso/image.iso /mnt/loop
sudo mount /dev/sdc1 /opt/mnt1
```

where `/dev/sdc1` is a formatted FAT32 partition on the USB drive

# Chroot into Linux from LiveCd

Rule is to mount `/dev`, `/proc`, `/sys` with binding option under the `/mnt`
where your system is installed (the one you want to chroot into).

```
sudo mount -o bind /dev /mnt/dev
sudo mount -o bind /proc /mnt/proc
sudo mount -o bind /sys /mnt/sys
```
