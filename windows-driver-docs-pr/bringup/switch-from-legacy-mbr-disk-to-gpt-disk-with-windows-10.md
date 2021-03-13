---
title: 通过 Windows 10 从旧式 MBR 磁盘切换到 GPT 磁盘
description: 提供有关启用无缝升级并使用户能够利用 Windows 10 的新的和改进的安全功能的指南。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: abcc2278316aac8c337078be99b62efc1699a981
ms.sourcegitcommit: 14c02f38dcdc4e2f3de2e3f6f4b554d87b08f3d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2021
ms.locfileid: "103442243"
---
# <a name="switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10"></a>通过 Windows 10 从旧式 MBR 磁盘切换到 GPT 磁盘

为了便于从下层操作系统（如 Windows 7）升级，或者从 BIOS 启动过渡到 UEFI Boot 以实现增强的安全功能。 Microsoft 提供了以下信息。 以下各节中的步骤将支持更无缝地升级到 Windows 10，并使用户能够利用 Windows 10 的新功能和改进的安全功能。 出于以下步骤的目的，我们将 GUID 分区表称为 GPT，将旧的主启动记录称为旧的 MBR 启动磁盘。

将使用以下四种配置：

- 配置 \# 1-没有兼容性支持模块 (CSM) 或在固件中禁用 csm 的 UEFI 启动。 需要 GPT 硬盘驱动器 (HDD) 。
- 配置 \# 2-启用了 CSM 的 UEFI 启动，从 GPT HDD 启动
- 配置 \# 3-启用了 CSM 的旧式 BIOS 启动，从旧 MBR HDD 启动
- 配置 \# 4-启用了 CSM 的 UEFI 启动，从旧 MBR HDD 启动

## <a name="upgrade-paths"></a>升级路径

| 现有 OS 和配置 | 目标操作系统和配置 | 结果 | 安全选项 |
|--|--|--|--|
| Windows 7 **x64** 已安装到带有 UEFI 固件的系统，在 GPT HDD 上启用 CSM (Config \# 2)  | Windows 10 **x64** 已安装到 GPT HDD 上启用的 UEFI 固件 CSM (Config \# 2)  | 将启动并运行 Windows 10 操作系统 | 禁用 CSM 后，操作系统才能使用固件中支持的 MS 安全功能 |
| Windows 7 **x64** 安装到带有活动分区 NTFS HDD 的 BIOS (Config \# 3)  | Windows 10 **x64** 已安装到带有活动分区 NTFS HDD 的 BIOS (Config \# 3)  | 将启动并运行 Windows 10 操作系统 | 仅能利用 Bitlocker |
| Windows 7 **x86** 已安装到带有活动分区 NTFS HDD 的 BIOS (Config \# 3)  | 使用有效分区 NTFS HDD = (安装到 BIOS 的 Windows 10 **x86** \#)  | 将启动并运行 Windows 10 操作系统 | 仅能利用 Bitlocker |
| Windows 7 **x86** 安装到带有活动分区的 BIOS (Config \# 3)  | Windows 10 **x64** 已安装到带有活动分区 NTFS HDD 的 BIOS (Config \# 3)  | 需要安装媒体并进行全新安装。 | 仅能利用 Bitlocker (其他安全功能需要 UEFI 启动)  |
| Windows 7 **x64** 安装到带活动分区的 BIOS (Config \# 3)  | Windows 10 **x64** 已安装到 GPT HDD 上禁用的 UEFI 固件 CSM (Config \# 1)  | 下面的特殊说明 | OS 能够利用固件中支持的 MS 安全功能 |

## <a name="definition-of-terms"></a>术语定义

**兼容性支持模块 (CSM)** 通常可在固件中启用或禁用。 此模块有助于实现，但并不指示使用旧的主启动记录（ (MBR) 启动到活动分区。 根据 BIOS/固件启动选项，您可以启用 CSM 并仍选择使用 GPT 磁盘或旧 MBR 启动模式启动到 UEFI 启动模式。 Windows 7 启动 UEFI 需要启用 CSM 并将其加载到内存中。
*UEFI 启动* 不需要启用 CSM。 禁用 CSM 后，启动不会使用硬盘驱动器上的活动分区 (HDD) ，它确实使用了 EFI 系统分区 (ESP) ，它会在其中查找可识别的文件系统，如 FAT-FAT32 和启动文件。 可以在) NVRAM (boot000n) 或 b) 中使用 UEFI 规范定义的用于查找 efi 启动启动方法的回退引导方法来定义启动文件 (\\ \\ \\ 例如： bootx64) 此启动方法在配置的 NTFS 引导磁盘上不起作用。

**旧 MBR 启动** 无法识别 GUID 分区表 (GPT) 磁盘。 它需要活动分区并支持 BIOS 才能访问磁盘。 原容量和有限的硬盘驱动器大小和分区数。 在 UEFI 固件系统上，它需要启用 CSM 并将其加载到内存中，以便于活动分区启动。

## <a name="in-this-section"></a>本节内容

[新方法-Windows 10 版本1703及更高版本](new-method--windows-10--version-1703-and-later.md)

[MBR2GPT 工具测试指南](mbr2gpt-tool-test-guidance.md)

[旧方法-Windows 10 版本1607及更早版本](old-method--windows-10--version-1607-and-earlier.md)

[如何转换已安装的 x64 Windows 7 系统](how-to-convert-an-installed-x64-windows-7.md)

## <a name="related-resources"></a>相关资源

[Windows 10 规范](https://www.microsoft.com/windows/Windows-10-specifications)
