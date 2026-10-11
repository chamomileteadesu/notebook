# ArchLinux Installation Steps

1. Connect to the network
2. Set ntp
3. Use `lsblk -pf`, and memorize the name of the devices
4. Use `cfdisk` to partition
    - 1 partition using `elf system`
    - 1 partition using `linux filesystem`
5. Use `mkfs` to format each partition with the correct format
6. Mount root partition to /mnt
7. Create subvolume `/mnt/@`, `/mnt/@home` and `/mnt/@swap` if using btrfs
8. Unmount `/mnt`
9. Mount:
    - `mount -t btrfs -o subvol=/@,compress=zstd /dev/sda2 /mnt`
    - `mount --mkdir -t btrfs -o subvol=/@home,compress=zstd /dev/sda2 /mnt/home`
    - `mount --mkdir -t btrfs -o subvol=/@swap,compress=zstd /dev/sda2 /mnt/swap`
    - `mount --mkdir /dev/sda1 /mnt/boot`
    - If dual-system needed: `mount --mkdir /dev/nvme0n1p1 /mnt/winboot`
10. Use `df -h` to check mount status
11. Refresh keyring using `pacman -Sy archlinux-keyring`
12. Install basic system using `pacstrap -K /mnt base base-devel linux-zen linux-firmware btrfs-progs`
13. Install other software: `pacstrap /mnt networkmanager neovim sudo intel-ucode`
14. Create swap file: `btrfs filesystem mkswapfile --size 64g --uuid clear /mnt/swap/swapfile`
15. Enable swap file: `swapon /mnt/swap/swapfile`
16. Generate fstab file: `genfstab -U /mnt > /mnt/etc/fstab`
17. Change root: `arch-chroot /mnt`
18. Set hostname: `vi /etc/hostname`
19. Set time zone: `ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
20. Sync time: `hwclock --systohc`
21. Localize:
    - Edit `/etc/locale.gen`, uncomment `en-US` and `zh-TW`
    - Run `local-gen`
    - Edit `/etc/locale.conf`, insert `LANG=en_US.UTF-8`
22. Set root password with `passwd`
23. Install boot program:
    - `pacman -S grub efibootmgr os-prober`
    - `grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=archlinux`
    - Edit grub: `vi /etc/default/grub`
        1. Delete `quite` so that you can see the startup log
        2. Change `loglevel` to 5
        3. Uncomment the last line
    - Generate grub configuration: `grub-mkconfig -o /boot/grub/grub.cfg`
24. Exit chroot and reboot
25. Connect to the network: `systemctl enable --now NetworkManager`
26. Install something:
    - `pacman -S gnome-desktop gdm ghostty gnome-control-center gnome-software linux-headers`
    - If you prefer Kde Plasmas: `pacman -S plasma-dedsktop plasma-nm plasma-pa`
27. Add a user and set password for him/her
28. Use `EDITOR=nvim visudo` to enable that user to use sudo
29. Install GPU driver `pacman -Syu nvidia nvidia-utils nvidia-settings` if using Nvidia, skip this if using AMD(Linux has built-in AMD GPU driver)
30. Start desktop environment with `systemctl start gdm`
31. Enable desktop environment with `systemctl enable gdm`
32. Install fonts: `sudo pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji`
33. Enable multilib: `vi /etc/pacman.conf`, `sudo pacman -Syyu`
34. Install sound firmware: `sudo pacman -S sof-firmware alsa-firmware alsa-ucm-conf`
35. Install sound service: `sudo pacman -S pipewire pipewire-pulse pipewire-alsa pipewire-jack wireplumber`
36. Enable sound service: `systemctl --user enable --now pipewire pipewire-pulse wireplumber`
37. Install GUI management tool: `sudo pacman -S pavucontrol`
38. Install advanced network config tools: `sudo pacman -S network-manager-applet dnsmasq`
39. Install paru
40. Install common applications: `paru -S mission-center gnome-text-editor gnome-disk-utility gnome-clocks gnome-calculator loupe snapshot baobab showtime fragments file-roller foliate firefox gst-plugin-pipewire gst-plugins-good pacman-contrib amberol wine`
41. Input Method:
    - Install fcitx5: `paru -Syu fcitx5 fcitx5-chinese-addons fcitx5-rime fcitx5-configtool fcitx5-gtk fcitx5-qt`
    - Set environment:
        - GTK_IM_MODULE=fcitx
        - QT_IM_MODULE=fcitx
        - XMODIFIERS=@im=fcitx
42. Snapshot service:
    - Install timeshift
    - Enable cronie service
    - Setup timeshift settings
    - Pacman install grub-btrfs and enable it
