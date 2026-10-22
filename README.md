# my-efi-files — 32 位 UEFI (IA32) 启动文件

> 给「64 位 CPU + 32 位 UEFI 固件」的小主机用的 EFI 启动文件集合，例如 Foxconn Kangaroo 二代、InFocus KJ-ONE 以及各类 BayTrail / Cherry Trail 设备。

## 内容

```

├── bootia32.efi      # 32 位 UEFI 启动入口（固件只会找它）
├── grubia32.efi      # 32 位 GRUB

```

## 用途

这些设备只认 `\EFI\BOOT\BOOTIA32.EFI`，而绝大多数 Linux 发行版（包括飞牛 fnOS）的安装 ISO
只带 64 位的 `bootx64.efi`，所以 32 位 UEFI 机器插上 U 盘会黑屏或直接回 BIOS。

把整个 `EFI` 目录拷到 U 盘根目录即可让固件找到启动入口：

```bash
cp -r EFI /mnt/usb/
```

安装完成后，还要把 `bootia32.efi` / `grubia32.efi` 复制到目标系统的 ESP：

```bash
sudo mkdir -p /boot/efi/EFI/BOOT
sudo cp EFI/BOOT/bootia32.efi EFI/BOOT/grubia32.efi /boot/efi/EFI/BOOT/
```

## 配合 fnOS 安装盘使用

手工改 ISO + 装完手动复制比较麻烦，可以直接用：

- [fnos-uefi32](https://github.com/txhtxh11/fnos-uefi32) —— 一条命令把这两个文件打进 fnOS 安装 ISO，
  并在安装过程中自动复制到目标 ESP

## 许可证

本项目采用 MIT 许可证，详见 [LICENSE](LICENSE)。
