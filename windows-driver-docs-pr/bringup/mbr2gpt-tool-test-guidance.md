---
title: MBR2GPT 工具测试指南
description: MBR2GPT 工具测试指南
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 434cf876f6e88e7a913a3acad2e44321b580d9a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337602"
---
# <a name="mbr2gpt-tool-test-guidance"></a>MBR2GPT 工具测试指南


**MBR2GPT.EXE** 可将磁盘从主启动记录 (MBR) 转换为 GUID 分区表 (GPT) 分区形式，无需修改或删除磁盘上的数据。 该工具旨在从 Windows 预安装环境 (Windows PE) 命令提示符下运行，但也可以从完整 Windows 10 操作系统 (OS) 运行。

有关该工具的详细说明，包括使用情况信息和故障排除指南，请查看 Technet 文章中的文档[MBR2GPT](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)。

## <a name="sample-checklist-when-verifying-conversion-from-biosmbr-to-uefigpt"></a>验证从 BIOS/MBR 转换为 UEFI/GPT 时的示例检查清单

- 运行 MBR2GPT 之前
    - 运行 msinfo32 以验证当前在 BIOS 模式下启动计算机
    - 运行 msinfo32 验证已安装 Windows 64 位操作系统
    - 使系统磁盘具有最多 3 个主分区在 MBR 和至少其中一个分区被标记为处于活动状态。
    - 请确保设备的固件支持 UEFI 引导，通过查找中的固件菜单中，相关的其他设置或检查与 PC/固件制造商
- 在运行 MBR2GPT，但在之前引导到 Windows 10 在 UEFI 模式下
    - 在固件菜单上，请确保启动模式设置设置为"仅限 UEFI"（或等效项）
    - 在固件菜单上，请确保兼容性支持模块 (CSM) 禁用和启用安全启动
- 在 UEFI 模式下启动到 Windows 10 后
    - 运行 msinfo32 以验证在 UEFI 模式下启动设备并启用安全启动
    - 验证你的业务线 (LOB) 应用程序的行仍在正常

**请注意**系统固件可以改变由制造商和设备。 如果有问题或顾虑，设备制造商联系以获得帮助。

## <a name="test-scenarios"></a>测试方案

### <a name="conversion-after-an-in-place-upgrade"></a>转换后的就地升级

1.  开始在 BIOS 模式下运行 Windows 7、 8 或 8.1 的设备。

2.  将设备升级到 Windows 10，版本 1507年、 1511 或版本 1607 在 BIOS 模式下。

3.  启动进入 Windows PE，版本 1703，它可以从 Windows 评估和部署工具包适用于 Windows 10，版本 1703年中获取的设备。

4.  运行 MBR2GPT。针对 Windows 10 的安装位置的磁盘的 EXE。

5.  重新配置固件在 UEFI 模式下启动、 启用安全启动和禁用 CSM 通过：

    - 更改固件菜单中的相关设置

    或

    - 运行 PC 或固件制造商提供的工具

6.  在 UEFI 模式下启动到 Windows 10

### <a name="conversion-as-part-of-re-imaging"></a>重置映像的一部分的转换

1.  开始在 BIOS 模式下运行 Windows 7、 8 或 8.1 的设备。

2.  捕获数据和设置，请使用 USMT 扫描状态。

3.  启动进入 Windows PE，版本 1703，它可以从 Windows 评估和部署工具包适用于 Windows 10，版本 1703年中获取的设备。

4.  部署 Windows 10，版本 1703年映像。

5.  运行 MBR2GPT。针对 Windows 10 的安装位置的磁盘的 EXE。

6.  重新配置固件在 UEFI 模式下启动、 启用安全启动和禁用 CSM 通过：

    - 更改固件菜单中的相关设置

    或

    - 运行 PC 或固件制造商提供的工具

7.  在 UEFI 模式下启动到 Windows 10

还原数据和设置，请使用 USMT 加载状态。

### <a name="conversion-as-part-of-hyper-v-generation-1-vm"></a>转换作为一部分的 HYPER-V 第 1 代 VM

1.  开始在 BIOS 模式下运行 Windows 7、 8 或 8.1 的设备。

2.  升级到 Windows 10 版本 1507年、 1511 或版本 1607 在 BIOS 模式下的 VM。

3.  启动进入 Windows PE，版本 1703，它可以从 Windows 评估和部署工具包适用于 Windows 10，版本 1703年中获取的 VM。

4.  针对你想要执行此转换的磁盘编号运行 MBR2GPT.exe。

5.  分离 VHD

6.  创建的生成 2 个 VM 使用 UEFI 支持和附加的上面的步骤 5 中创建的上述 VHD。

7.  启动到 Windows 10，版本 1703年在 UEFI 模式下使用 gen 2 VM。

**请注意**对于任何上述方案中，你可以转换 MBR 磁盘使用 BitLocker 加密卷，前提是已挂起保护。 要在转换后恢复 BitLocker，需要删除现有保护程序并重新创建。

## <a name="troubleshooting"></a>疑难解答

请参阅 MBR2GPT。EXE[故障排除](https://docs.microsoft.com/windows/deployment/mbr-to-gpt#troubleshooting)文档了解有关日志文件位置和其他帮助信息。 如果您将自动使用此工具通过脚本或 SCCM/MDT 任务序列，可以编写脚本的处理程序返回文档中讨论的代码。

## <a name="related-resources"></a>相关资源

[MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)



