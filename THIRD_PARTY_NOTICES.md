# 第三方组件声明（THIRD PARTY NOTICES）

本文件说明 **WiKey 跑包工具**（WiKey CrackTool）在 Windows 发布包中随包分发的第三方
组件、其著作权归属、许可条款以及本软件对这些条款的遵守方式。

本文件本身不授予对第三方组件的任何权利。对这些组件的使用受其各自许可条款约束；
这些条款的完整文本随包附带，位置见下表"许可文本位置"一列。

本软件自身的许可见 [LICENSE](LICENSE)。

---

## 一、随外部工具目录分发的组件（`bin/`）

### 1. hashcat 7.1.2

| 项目 | 内容 |
| --- | --- |
| 组件 | hashcat 密码恢复引擎 |
| 著作权人 | Jens Steube |
| 版权声明 | Copyright (c) 2015-2025 Jens Steube |
| 许可 | **MIT License** |
| 随包内容 | `bin/hashcat/hashcat.exe` 及其 1850 个资源文件（OpenCL 内核、模块、规则、掩码、字符集、调优文件等） |
| 许可文本位置 | `bin/hashcat/docs/license.txt` |

**MIT 条款要求**：在软件的所有副本或实质性部分中保留版权声明与许可声明。本软件通过
随包附带上述 `license.txt` 原文满足该要求，未作任何删改。

hashcat 自身使用的第三方库与组件，其许可条款与著作权人列于 `bin/hashcat/docs/license_libs/`：

- `LZMA_SDK_LICENSE.txt` — LZMA SDK（7-Zip SDK，公共领域/LGPL 双许可）
- `MINIZ_LICENSE.txt` — miniz
- `OPENCL_HEADERS_LICENSE.txt` — OpenCL headers
- `SSE2NEON_LICENSE.txt` — SSE2NEON
- `UNRAR_LICENSE.txt` — unRAR（**含 unRAR 许可限制**，见下节）
- `XXHASH_LICENSE.txt` — xxHash
- `ZLIB_LICENSE.txt` — zlib

### 2. 7-Zip 26.02

| 项目 | 内容 |
| --- | --- |
| 组件 | 7-Zip 命令行与解压缩库 |
| 著作权人 | Igor Pavlov |
| 版权声明 | 7-Zip Copyright (C) 1999-2026 Igor Pavlov；unRAR 原始代码版权归 Alexander Roshal 所有 |
| 许可 | **GNU LGPL v2.1**（含 **unRAR 许可限制**部分代码）与 **BSD 3-clause / BSD 2-clause**（部分代码） |
| 随包内容 | `bin/7zip/7z.exe`、`bin/7zip/7z.dll` |
| 许可文本位置 | `bin/7zip/License.txt` |

**7-Zip 条款要求**：以二进制形式再分发时，必须复制该文件中的相关许可信息。本软件通
过随包附带未删改的 `License.txt` 满足该要求。

**unRAR 许可限制**：7-Zip 的 RAR 解压引擎使用了 unRAR 程序的源代码，unRAR 原始代码
版权归 Alexander Roshal 所有，其许可附带如下限制（原文见 `bin/7zip/License.txt` 的
"unRAR license restriction"一节）：

> The unRAR sources cannot be used to re-create the RAR compression algorithm, which is
> proprietary. Distribution of modified unRAR sources in separate form or as a part of other
> software is permitted, provided that it is clearly stated in the documentation and source
> comments that the code may not be used to develop a RAR (WinRAR) compatible archiver.

本软件遵守该限制：**不将** unRAR 代码或 `7z.dll` 用于重建 RAR 压缩算法，**不**用于开
发任何 RAR（WinRAR）兼容的压缩器。`7z.dll` 在本软件中仅用于**解包**已分发的发布包与
用户自行处理的归档文件。

---

## 二、冻结进 Windows 可执行文件的组件

以下 Python 包在构建时被冻结进 `WiKey跑包工具.exe`（PyInstaller one-file 打包）。

### 3. Qt 6（经由 PySide6 6.3.0）

| 项目 | 内容 |
| --- | --- |
| 组件 | Qt 6 基础库与 Qt Widgets |
| 著作权人 | The Qt Company Ltd. and contributors |
| 许可 | **GNU LGPL v3**（亦可选择 GPL v3 或商业许可） |
| 随包内容 | `resources/PySide6/Qt6Core.dll`、`Qt6Gui.dll`、`Qt6Network.dll`、`Qt6OpenGL.dll`、`Qt6Svg.dll`、`Qt6SvgWidgets.dll`、`Qt6Widgets.dll`、对应 `.pyd` 绑定模块、`plugins/`、`translations/` |

**遵守方式**：Qt 库以**独立动态链接库（DLL）**形式随包分发，未静态链接进可执行文件。
使用者可以自由替换、升级或对这些 Qt 动态库重新链接，从而运行本软件的修改版本。本软
件未设置任何阻止使用者为调试自身修改而逆向工程 Qt 库的技术限制措施，也未附加任何
以阻止上述替换或逆向为目的的附加条件。

### 4. PySide6 6.3.0 与 shiboken6

| 项目 | 内容 |
| --- | --- |
| 著作权人 | The Qt Company Ltd. and contributors |
| 许可 | **GNU LGPL v3**（亦可选择 GPL v3 或商业许可） |
| 随包内容 | `pyside6.abi3.dll` 与 Qt 绑定模块 |

遵守方式同第 3 节（以独立动态库形式随包，允许替换与重新链接）。

### 5. Mesa 3D（llvmpipe 软件 OpenGL 实现）

| 项目 | 内容 |
| --- | --- |
| 组件 | `opengl32sw.dll`（Qt 附带的 Mesa llvmpipe 软件渲染后端） |
| 著作权人 | Mesa 3D Contributors |
| 许可 | **MIT License** |

MIT 条款要求的版权与许可声明保留在该组件随附的许可信息中。

### 6. psutil

| 项目 | 内容 |
| --- | --- |
| 组件 | 进程与系统资源查询库 |
| 许可 | **BSD 3-Clause License** |

BSD 条款要求保留版权、条件和免责声明声明；本软件未对该组件作任何修改地随包分发。

### 7. Python 3.10.11（标准库）

| 项目 | 内容 |
| --- | --- |
| 组件 | Python 解释器及其标准库（冻结进可执行文件） |
| 著作权人 | Python Software Foundation 及贡献者 |
| 许可 | **PSF License Agreement**（PSF-2.0） |

PSF 许可不要求本软件公开其自身源代码；本软件亦未对 Python 标准库作任何修改。

### 8. PyInstaller 6.20.0（bootloader）

| 项目 | 内容 |
| --- | --- |
| 组件 | 冻结打包用的 bootloader 引导程序 |
| 许可 | **GPL v2 + bootloader 例外条款（Bootloader Exception）** |

PyInstaller 的 bootloader 例外条款明确允许将 bootloader 与使用 PyInstaller 打包的
应用程序一并分发，且**不要求**公开该应用程序的源代码。

---

## 三、仅构建期使用、不随包分发

| 组件 | 许可 | 用途 |
| --- | --- | --- |
| pyinstaller-hooks-contrib 2026.5 | GPL v2（带例外）/ MIT | 构建期钩子 |
| pefile 2024.8.26 | MIT | 构建期 PE 依赖检查 |

上述构建期依赖不随发布包分发，其完整版本清单仅存在于私有源码仓库。

---

## 四、许可兼容性说明

本软件为保留所有权利的专有软件。上述第三方组件均以独立可执行文件、独立动态链接
库或经批准的宽松许可条款授权，其条款与本软件的专有许可不冲突：第三方组件的许可
不适用于本软件的专有代码，本软件的专有许可亦不影响第三方组件按其条款所享有的权
利。Qt 及 PySide6 以动态链接方式使用，符合 LGPL v3 关于以可替换的独立库形式提供
作品的合规要求。
