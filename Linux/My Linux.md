# Installation

Using Arch linux USB boot media
## 1. Check boot method

```bash
ls /sys/firmware/efi/efivars
```

should be shown without any errors
## 2. Connect to the network (WiFi)

```bash
iwctl
device list
station [device] scan
station [device] get-networks
station [device] connect [network]
exit

ping -c 1 archlinux.org
```
## 3. Partition disks

```
fdisk [disk]
```
### 3-1. `fdisk` options
- `m`: display menu
- `g`: make partition table to gpt
- `n`: make new partition
- `t`: set partition type
- `p`: display current partitions
- `w`: save and exit
- `q`: exit without saving any changes
### 3-2. Partition example

| partition<br>               | partition kind       | size                  |
| --------------------------- | -------------------- | --------------------- |
| */dev/efi_system_partition* | EFI system partition | > 300Mib (required)   |
| */dev/swap_partition*       | Linux swap           | > 512Mib              |
| */dev/root_partition*       | Linux filesystem     | the rest part of disk |
## 4. Format partitions

| partition                   | format | command                                    |
| --------------------------- | ------ | ------------------------------------------ |
| */dev/efi_system_partition* | fat32  | `mkfs.fat -F 32 /dev/efi_system_partition` |
| */dev/swap_partition*       | swap   | `mkswap /dev/swap_partition`               |
| */dev/root_partition*       | ext4   | `mkfs.ext4 /dev/root_partition`            |
## 5. Mount partitions

| partition                   | mountpoint      | command                                        |
| --------------------------- | --------------- | ---------------------------------------------- |
| */dev/root_partition*       | `/mnt`          | `mount /dev/root_partition /mnt`               |
| */dev/efi_system_partition* | `/mnt/boot/efi` | `mount /dev/efi_system_partiton /mnt/boot/efi` |
| */dev/swap_partition*       | `[SWAP]`        | `swapon /dev/swap_partition`                   |
> [!WARNING]
> `/dev/root_partition` must be mounted before the `/dev/efi_syste_partition`

## 6. Install packages

```bash
pacstrap /mnt base linux linux-firmware grub efibootmgr networkmanager sof-firmware base-devel vim neovim
```

## 7. Config system
### fstab

```bash
getfstab -U /mnt >> /mnt/etc/fstab
```
### chroot

```bash
arch-chroot /mnt
```

### timezone

```bash
ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
hwclock --systohc
```

### locales
#### locale gen

```bash
nvim /etc/locale.gen
```

```bash
ko_KR.UTF-8 # uncommented
```

```bash
locale-gen
```
#### locale conf

```bash
nvim /etc/locale.conf
```

```bash
LANG=ko_KR.UTF-8
```
### hostname

```
nvim /etc/hostname
```

```
archlinux
```
### user
#### add new user

```bash
useradd -m -G wheel [user]
passwd [user]
```
#### make user as sudoer

```bash
visudo
```

```
%wheel ALL=(ALL) # uncommented
```
### networkmanager

```bash
systemctl enable networkmanager
```
### grub

```bash
grub-install /dev/efi_system_partition
grub-mkconfig -o /boot/grub/grub.cfg
```
## 

```
umount -a && reboot
```
# Post Installation

## DM

```bash
sudo pacman -S sddm
sudo systemctl enable sddm
```
## WM

```bash
sudo pacman -S hyprland
```

## Utilites

#### desktop apps

```bash
sudo pacman -S kitty dolphin wofi wl-clipboard mako pipewire wireplumber qt5-wayland qt6-wayland firefox
```
#### hyprland utils

```bash
sudo pacman -S hyprcursor hyprgraphics hyprland-qt-support hyprland-qtutils hyprlang hyprlock hyprpaper hyprshot hyprutils hyprwayland-scanner xdg-desktop-portal-hyprland
```
### fonts

```bash
sudo pacman -S noto-fonts-cjk ttf-nerd-fonts-symbols-common ttf-nerd-fonts-symbols-mono ttf-nerd-fonts-symbols
```
### networkmanager

```bash
sudo pacman -S network-manager-applet nm-connection-editor
```

```bash
nmcli device wifi list
nmcli device wifi connect [network] password [password]
```
### fcitx5

```bash
sudo pacman -S fcitx5-im fcitx5-hangul
```

