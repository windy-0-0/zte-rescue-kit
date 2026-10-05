# zte-rescue-kit

中兴 ZTE 7552N（畅行60 / P720S20）**救砖工具包 + 官方固件**

## 内容（共 459 个文件）

| 路径 | 说明 |
|---|---|
| `HCTSW_ZTE_7552N_13.0.18CN.pac` | 官方固件（6.58 GB），展锐线刷用 |
| `00-操作SOP-按顺序执行.md` | **按顺序执行的操作手册**（先读这个） |
| `救砖操作手册.md` | 救砖流程详解 |
| `固件下载信息.md` | 固件来源与下载链接 |
| `文件校验MD5.txt` | boot.bin / vbmeta.bin 的 MD5 |
| `ResearchDownload/` | 展锐线刷工具（含 Bin 可执行文件 + Source 源码 + Doc 手册） |
| `SPRD_Driver/` | 展锐 USB 驱动（Win10 x86/x64） |
| `boot.bin` / `vbmeta.bin` / `misc-wipe.bin` | 分区镜像 |
| `fdl1-dl.bin` / `fdl2-*.bin` / `splloader.bin` | 展锐下载模式引导文件 |
| `spd_dump.exe` | 展锐分区读写工具 |
| `ssh刷机脚本.bat` / `unlock_autopatch_9620_autodl.bat` | 自动化脚本 |
| `uboot_bak.bin` | U-Boot 备份 |

## ⚠️ 分片下载与还原

整个工具包以 **tar.gz 流 + 200MB 分片** 上传（含固件，总计约 5.9 GB 流）。

### 还原步骤

```bash
# 1. 下载全部分片
gh release download v1.0 -R windy-0-0/zte-rescue-kit -p "zte-rescue-part-*"

# 2. 合并并解压到当前目录
cat zte-rescue-part-* | tar xzf -

# 3. 校验关键镜像
md5 boot.bin      # 期望 7847ba157bc2b961a8d66657a71b1a4f
md5 vbmeta.bin    # 期望 71de3e90e7da89d52ff4386f59fa430f
```

### 分片清单

| 分片前缀 | 片数 | 流总字节 |
|---|---|---|
| `zte-rescue-part-aa` … `zte-rescue-part-bc` | 29 | 5,934,827,520 |

> 前 28 片各 200MB（209,715,200 字节），末片为余数。

## 救砖流程（概要）

> 详细步骤以包内 `00-操作SOP-按顺序执行.md` 为准。

1. 装展锐驱动 `SPRD_Driver/`
2. 手机进 download 模式（音量下 + 电源）
3. `ResearchDownload` 加载 `.pac` 整包线刷
4. 若分区损坏，用 `spd_dump.exe` 配合 `fdl1-dl.bin` / `fdl2-dl.bin` 单独写回

## 相关仓库

- [`zte-firmware`](https://github.com/windy-0-0/zte-firmware) — 仅固件（.pac + .7z 原包）

## 来源

固件来自 HCT_Nekobot（HikariCalyx 刷机团队）。仅供个人救砖使用。
