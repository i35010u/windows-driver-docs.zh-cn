---
title: 从旧版 MBR 磁盘切换到与 Windows 10 的 GPT 磁盘
description: 提供了指导启用无缝升级，并使用户能够利用 Windows 10 的新的和改进的安全功能。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98df70836d05e6f36c8dd8bac56d1e8e44b5c1f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337430"
---
# <a name="switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10"></a>从旧版 MBR 磁盘切换到与 Windows 10 的 GPT 磁盘

若要简化从下层操作系统，如 Windows 7 升级，或者从 BIOS 启动转换为 UEFI Boot 的增强的安全功能。 Microsoft 提供了以下信息。 以下部分中的步骤将启用更无缝升级到 Windows 10，并使用户能够充分利用 Windows 10 的新的和改进的安全功能。 对于以下步骤，我们将引用为 GPT，而 GUID 分区表和旧主启动记录作为旧版 MBR 启动盘。

将使用以下四种配置：

- 配置\#1-UEFI 启动不兼容性支持模块 (CSM) 或 CSM 禁用固件中。 需要 GPT 硬盘驱动器 (HDD)。
- 配置\#2-使用 CSM 启用，从 GPT 硬盘启动的 UEFI 引导
- 配置\#CSM 启用，从旧 MBR HDD 启动与 3-传统 BIOS 启动
- 配置\#4-使用 CSM 启用，从旧 MBR HDD 启动的 UEFI 引导

## <a name="upgrade-paths"></a>升级路径

| 现有 OS + 配置 | 目标 OS + 配置 | 结果 | 安全选项 |
| ---  |--- | --- | --- |
| Windows 7 **x64**安装到使用 UEFI 固件的系统，在 GPT 硬盘上启用 CSM (配置\#2) | Windows 10 **x64**安装到 UEFI 固件 CSM GPT HDD 上启用 (配置\#2)        | 将启动并运行 Windows 10 操作系统               | OS 是能够使用 MS 禁用 CSM 后在固件中支持的安全功能 |
| Windows 7 **x64**与活动分区 NTFS HDD 安装到 BIOS (配置\#3)               | Windows 10 **x64**与活动分区 NTFS HDD 安装到 BIOS (配置\#3)         | 将启动并运行 Windows 10 操作系统               | 仅可以利用 Bitlocker                                                           | 本文档不包括                                                                  |
| Windows 7 **x86**与活动分区 NTFS HDD 安装到 BIOS (配置\#3)               | Windows 10 **x86**与活动分区 NTFS HDD 安装到 BIOS = works (配置\#3) | 将启动并运行 Windows 10 操作系统               | 仅可以利用 Bitlocker                                                           | 本文档不包括                                                                  |
| Windows 7 **x86**与活动分区 NTFS 安装到 BIOS (配置\#3)                   | Windows 10 **x64**与活动分区 NTFS HDD 安装到 BIOS (配置\#3)         | 需要安装媒体和全新安装。 | 仅可以利用的 Bitlocker （其他安全功能需要 UEFI 引导）               |
| Windows 7 **x64**与活动分区 NTFS 安装到 BIOS (配置\#3)                   | Windows 10 **x64**安装到 UEFI 固件在 GPT 硬盘上禁用 CSM (配置\#1)        | 下面的特殊说明                      | OS 是能够使用 MS 固件中支持的安全功能

## <a name="definition-of-terms"></a>术语的定义

**兼容性支持模块 (CSM)** 通常可以启用或禁用固件中。 此模块方便了，但不要求启动到活动与旧的主启动记录 (MBR) 分区。 根据 BIOS/固件启动选项，您可能能够启用 CSM 并仍选择启动到 UEFI 启动模式下使用 GPT 磁盘或旧版 MBR 启动模式。 具有 CSM 启用并加载到内存，则需要适用于 Windows 7 启动 UEFI。
*UEFI 引导*不需要 CSM 才可用。 禁用 CSM，启动时不使用硬盘 Drive(HDD) 上的一个活动分区，这样做以后使用，它可在其中查找可识别的文件系统，如 FAT FAT32 启动文件与 EFI 系统分区 (ESP)。 可以将启动文件定义中) NVRAM (boot000n) 或 b） 使用 UEFI 规范定义回退启动方法寻找\\EFI\\启动\\启动 （体系结构）.efi (例如： bootx64.efi) 此引导方法不适用于旧的 MBR 配置 NTFS 启动磁盘。

**旧的 MBR 启动**无法识别的 GUID 分区表 (GPT) 磁盘。 它需要一个活动分区，并支持 BIOS 以便访问磁盘。 旧、 最有限 HDD 大小和数量的分区。 UEFI 固件在系统上，它需要 CSM 启用并加载到内存，以便启动活动分区。

## <a name="in-this-section"></a>本节内容

[新方法-Windows 10 版本 1703年及更高版本](new-method--windows-10--version-1703-and-later.md)

[MBR2GPT 工具测试指南](mbr2gpt-tool-test-guidance.md)

[旧方法-Windows 10 版本 1607年及更早版本](old-method--windows-10--version-1607-and-earlier.md)

[如何将转换已安装的 x64 Windows 7 系统](how-to-convert-an-installed-x64-windows-7.md)

## <a name="related-resources"></a>相关资源

[Windows 10 规范](https://www.microsoft.com/windows/Windows-10-specifications)
