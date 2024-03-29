# Arch 1st

loadkeys us

loadkeys ru

### 1) create partitions fdisk (cfdisk)
        a - boot
        n - create
        p - view
        t - type
        swap = 82
        
 ##### create logical partitions like LVM
 ```nginx
 pvcreate /dev/sda2
 vgreate vg_host_sys /dev/sda2
 lvcreate -L 20G vg_host_sys -n lv_root
        .....
  ```      
  ### 2) format filysystem
  ```nginx
 mkfs.ext4 /dev/mapper/vg_host_sys-lv_root
 mkfs.ext2 /dev/mapper/vg_host_sys-lv-boot     or    /dev/sdaX (2 method for two or more grub)
 .....
 mkswap /dev/mapper/vg_host_sys-lv_swap        or    /dev/sdaX (2 method for dual or more linux OS)
  ```     
  ### 3) mount partitions
  ```nginx
 mount /dev/mapper/vg_host_sys-lv-root /mnt
 mkdir /mnt/{boot,home,opt,var}
 mkdir -p /mnt/usr/{local,share}
   ```     
 ### 4) Prepare to download and dowload packages      
       
* /etc/pacman.d/mirrorlist
```nginx 
                            |--> передвинуть вверх (-> RU) or (yandex)
```
```nginx
pacstrap -i /mnt base base-devel sudo net-tools gvim openssh git
genfstab -U -p /mnt >> /mnt/etc/fstab
#cp install.txt /mnt/root
arch-chroot /mnt
```      
### 5) arch-chroot settings
```nginx
echo archlinux > /etc/hostname
ln -sf /usr/share/zoneinfo/Europe/Moscow /etc/localtime
vim /etc/locale.gen   
                   |-->  en_US.UTF-8;ru_RU.UTF-8 + KOIR8 (если проблемы и начались символы оставить KOIR или LC_messages english)
 ```

* /etc/locale.conf
```nginx
                  |-->  LANG=ru_RU.UTF-8
                        LANGUAGE=ru_RU.UTF-8:en_US.UTF-8
                        LC_MESSAGES=en_US.UTF-8
```
```nginx
hwclock --systohc --utc
locale-gen
#locale >> /etc/locale.conf
```
* /etc/vconsole.conf
```nginx
                  |--> KEYMAP=us
                       KEYMAP=ru
```
```nginx
pacman –Sy lvm2 grub intel-ucode os-prober        (or "efibootmgr" if use efi instead bios)
```
* /etc/mkinitcpio.conf
```nginx
                      |-->  line HOOKS="..... add to END
                                    -> keymap
                                               and add after block 
                                    -> lvm2
                                               and add to end shutdown #resolve problem systemd "/var"
                            line like this:
                                    :-> HOOKS=(base udev autodetect modconf block lvm2 filesystems keyboard fsck keymap shutdown)       
```
* /etc/modprobe.d/blacklist.conf
```nginx
                                |-->   blacklist pcspkr
```                                
```nginx                      
mkinitcpio -p linux
```
* /etc/default/grub
```nginx
                   |-->  line GRUB_PRELOAD_MODULES="... add to end
                                      -> lvm
                         line like this 
                                      :-> GRUB_PRELOAD_MODULES="part_gpt part_msdos lvm"
```                 
 ### 6) grub install ( miss this if you have ubuntu or other linux OS  (in ubuntu sudo update-grub) )
 ```nginx
grub-install /dev/sdA (no sda1 or sda3 ....)
#pacman -S os-prober
grub-mkconfig -o /boot/grub/grub.cfg
passwd root
```        
 ### 7) unmounting
```nginx 
umount -lR /mnt
reboot
```
