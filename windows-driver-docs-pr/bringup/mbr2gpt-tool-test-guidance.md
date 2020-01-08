---
title: MBR2GPT 工具测试指南
description: MBR2GPT 工具测试指南
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62c68c1baba40467530339ffdcdd96ff4111163e
ms.sourcegitcommit: 9b764ce48a3af451528a4229cdfb62221ef56942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75607677"
---
# <a name="mbr2gpt-tool-test-guidance"></a>MBR2GPT 工具测试指南

**MBR2GPT.EXE** 可将磁盘从主启动记录 (MBR) 转换为 GUID 分区表 (GPT) 分区形式，无需修改或删除磁盘上的数据。 该工具旨在从 Windows 预安装环境（Windows PE）命令提示符中运行，但也可以从完整的 Windows 10 操作系统（OS）中运行。

有关详细的使用情况信息和故障排除指南，请参阅[mbr2gpt.exe](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)文档。

## <a name="sample-checklist-when-verifying-conversion-from-biosmbr-to-uefigpt"></a>验证从 BIOS/MBR 到 UEFI/GPT 的转换时的示例清单

- 在运行 MBR2GPT.EXE 之前
  - 运行 msinfo32 以验证计算机当前是否在 BIOS 模式下启动
  - 运行 msinfo32 以验证是否安装了 Windows 64 位操作系统
  - 请确保系统磁盘最多有3个主分区，并将至少一个分区标记为 "活动"。
  - 通过在 "固件" 菜单中查找相关设置，或者通过检查 PC/固件制造商，确保设备的固件支持 UEFI boot
- 运行 MBR2GPT.EXE 之后，但在 UEFI 模式下启动到 Windows 10 之前
  - 在固件菜单中，确保将 "启动模式" 设置设为 "仅 UEFI" （或等效项）
  - 在固件菜单中，确保禁用兼容性支持模块（CSM）并启用安全启动
- 在 UEFI 模式下启动到 Windows 10 后
  - 运行 msinfo32 以验证设备是否在 UEFI 模式下启动，以及是否启用了安全启动
  - 验证你的业务线（LOB）应用程序是否仍正常工作

> [!NOTE]
> 系统固件可能因制造商和设备而异。 如果有疑问或问题，请与设备制造商联系以获得帮助。

## <a name="test-scenarios"></a>测试方案

### <a name="conversion-after-an-in-place-upgrade"></a>就地升级后的转换

1. 从运行 Windows 7、8或8.1 的设备开始，在 BIOS 模式下运行。

1. 在 BIOS 模式下将设备升级到 Windows 10 版本1507、版本1511或版本1607。

1. 将设备启动到 Windows PE 版本1703，该版本可从适用于 Windows 10 的 Windows 评估和部署工具包（版本1703）中获取。

1. 运行 MBR2GPT.EXE。EXE 中安装了 Windows 10 的磁盘。

1. 重新配置固件以在 UEFI 模式下启动，启用安全启动，并通过以下方式禁用 CSM：

    - 更改固件菜单中的相关设置

    或

    - 运行电脑或固件制造商提供的工具

1. 在 UEFI 模式下启动到 Windows 10

### <a name="conversion-as-part-of-re-imaging"></a>作为重新映像的一部分转换

1. 从运行 Windows 7、8或8.1 的设备开始，在 BIOS 模式下运行。

1. 使用 USMT 扫描状态捕获数据和设置。

1. 将设备启动到 Windows PE 版本1703，该版本可从适用于 Windows 10 的 Windows 评估和部署工具包（版本1703）中获取。

1. 部署 Windows 10 版本1703映像。

1. 运行 MBR2GPT.EXE。EXE 中安装了 Windows 10 的磁盘。

1. 重新配置固件以在 UEFI 模式下启动，启用安全启动，并通过以下方式禁用 CSM：

    - 更改固件菜单中的相关设置

    或

    - 运行电脑或固件制造商提供的工具

1. 在 UEFI 模式下启动到 Windows 10

使用 USMT 加载状态还原数据和设置。

### <a name="conversion-as-part-of-hyper-v-generation-1-vm"></a>作为 Hyper-v 第1代 VM 的一部分转换

1. 从运行 Windows 7、8或8.1 的设备开始，在 BIOS 模式下运行。

1. 在 BIOS 模式下将 VM 升级到 Windows 10 版本1507、版本1511或版本1607。

1. 将 VM 启动到 Windows PE 版本1703，该版本可从适用于 Windows 10 的 Windows 评估和部署工具包（版本1703）中获得。

1. 针对要执行转换的磁盘编号运行 MBR2GPT.EXE。

1. 分离 VHD

1. 使用 UEFI 支持创建第2代 VM，并附加上面步骤5中创建的上述 VHD。

1. 使用第2代 VM 在 UEFI 模式下启动到 Windows 10 1703 版。

> [!NOTE]
> 对于上述任何方案，只要保护已挂起，就可以使用 BitLocker 加密的卷来转换 MBR 磁盘。 要在转换后恢复 BitLocker，需要删除现有保护程序并重新创建。

## <a name="troubleshooting"></a>“疑难解答”

请参阅 MBR2GPT.EXE。EXE[疑难解答](https://docs.microsoft.com/windows/deployment/mbr-to-gpt#troubleshooting)文档，了解有关日志文件位置和其他帮助的信息。 如果通过脚本或 Microsoft Endpoint Configuration Manager/Microsoft 部署工具包（MDT）任务序列自动使用此工具，则可以为文档中讨论的返回代码编写处理程序。

## <a name="related-resources"></a>相关资源

[MBR2GPT.EXE..EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)
