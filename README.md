# loongarch-gpu-drivers

LoongArch (loong64) GPU 驱动 Arch Linux 打包仓库。

为龙芯平台提供完整的 GPU 图形驱动支持，面向 **New World**（上游内核 ABI）系统。

## 包含的包

| 包名 | 类型 | 说明 |
|------|------|------|
| `linux-firmware-loongson` | 固件 | lg100/lg200 GPU 固件 (CP microcode) |
| `libldrm` | 用户态库 | LDROM 运行时库 + loonggpu 设备 ID 表 |
| `libloong-gpucomp` | 用户态库 | GPUCOMP 运行时库 |
| `loonggl` | 用户态库 | 二进制 OpenGL / OpenGL ES / EGL / GLX 实现 |
| `loonggpu-dkms` | 内核模块(DKMS) | loonggpu + loonggpu-bridge 内核模块 |
| `xf86-video-loonggpu` | Xorg 驱动 | Xorg video driver + DRI 驱动 |
| `loonggpu-settings` | 配置 | `/etc/loonggpu/loonggpu_driver.conf` |
| `loonggpu-driver` | 元包 | 一键安装上述全部包 |

## 安装

```bash
# 一键安装全部驱动
makepkg -si -p loonggpu-driver/PKGBUILD

# 或逐个安装（按依赖顺序）
cd linux-firmware-loongson && makepkg -si && cd ..
cd libldrm              && makepkg -si && cd ..
cd libloong-gpucomp     && makepkg -si && cd ..
cd loonggl              && makepkg -si && cd ..
cd loonggpu-dkms        && makepkg -si && cd ..
cd xf86-video-loonggpu  && makepkg -si && cd ..
cd loonggpu-settings    && makepkg -si && cd ..
```

## 注意事项

- 所有闭源二进制包来自 [Loongnix 25 仓库](https://pkg.loongnix.cn/loongnix/25/pool/non-free/l/loonggpu-graphics-drivers/)
- `loonggpu-dkms` 使用 [AOSC-Tracking/loonggpu-kernel-dkms](https://github.com/AOSC-Tracking/loonggpu-kernel-dkms) 源码，包含针对上游内核 v6.18+ 的适配补丁
- `xf86-video-loonggpu` 中创建了 `libedit.so.2` 兼容 symlink（Arch 的 `libedit` 提供 `libedit.so`）
- 本仓库的 PKGBUILD 和配置文件采用 **GPL-3.0-or-later** 许可证（参见 LICENSE 文件）
- 打包的二进制驱动本身为 Loongson 专有软件，适用 `custom:LOONGGPU` 许可证

## 硬件

已知支持的 GPU 芯片（需结合主板/SoC 确认）：

| 芯片 | 对应固件 |
|------|----------|
| LG100 系列 | `lg100_cp.bin` |
| LG200 系列 | `lg200_cp.bin` |
