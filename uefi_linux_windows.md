# Install Ubuntu alongside Windows10 - UEFI

- check if BIOS(?) is set to **UEFI-only** boot! Very important! No legacy shit.
- make some room for Ubuntu on the disk
- prepare bootable USB with **GPT** partition table + **boot** flag! Very important!
- you can create bootable USB from any bootable ISO image by:

To check if you're on **UEFI-only** settings, please execute
```
efibootmgr
```

if you'll see `efibootmgr: EFI variables are not supported on this system.`
that means there's something wrong with your UEFI settings and you should review
your BIOS.

Using `efibootmgr` you can change the Boot order.


## Create bootable USB from any bootable ISO
```bash
sudo mkdir -p /mnt/{loop, mnt1}
sudo mount -o loop /opt/iso/image.iso /mnt/loop
sudo mount /dev/sdc1 /opt/mnt1
```

where `/dev/sdc1` is a formatted FAT32 partition on the USB drive. And then just copy (or `rsync` with symlinks) the content of `/mnt/loop` to the `/mnt/mnt1`.



# Chroot into Linux from LiveCd

Rule is to mount `/dev`, `/proc`, `/sys` with binding option under the `/mnt`
where your system is installed (the one you want to chroot into).
```bash
sudo mount -o bind /dev /mnt/dev
sudo mount -o bind /proc /mnt/proc
sudo mount -o bind /sys /mnt/sys
```



# Troubleshooting

## Freezing Ubuntu installation on modern notebooks with UEFI
During the LiveCD/USB booting, if you encountered some freezing, try the following.
Edit GRUB entry for launching ubuntu and replace `quiet splash ---` with `nomodest`.

You may also want to change the default GRUB settings in `/etc/default/grub`.

Don't forget to execute `update-grub` after making changes in GRUB config.


## Black screen after successful installation
```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt-get update
sudo apt-get install -y boot-repair && boot-repair
```
