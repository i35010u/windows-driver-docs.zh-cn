---
title: 固件 Windows 工程指南 (WEG)
description: 固件 Windows 工程指南 (WEG) 提供了实施系统固件相关的最佳实践中应遵循的步骤。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc5fd86aa82665f574d42dde95d2a998a4cd2a02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546535"
---
# <a name="firmware-windows-engineering-guide-weg"></a>固件 Windows 工程指南 (WEG)

固件 Windows 工程指南 (WEG) 提供了实施系统固件相关的最佳实践中应遵循的步骤。


## <a name="in-this-section"></a>本部分内容

[UEFI 安全](uefi-security.md)

[固件更新](firmware-update.md)

[SMBIOS](smbios.md)

[HTTPS](https-boot.md)

[在固件中的 Wi-fi 支持](wi-fi-support-in-firmware.md)

[从旧的 MBR 磁盘切换到与 Windows 10 的 GPT 磁盘](switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10.md)

[固件 WEG 常见问题](frequently-asked-questions.md)

[为 Windows 7 和更高版本更新适用于 Windows 10 配置系统固件](configure-system-firmware-for-windows-7-and-later-update-for-windows-10.md)

[示例 PowerShell 脚本保存到本地查询 SMBIOS](sample-powershell-script-to-query-smbios-locally.md)

                                           





## <a name="firmware-weg-terminology"></a>固件 WEG 术语

以下术语在整个固件 WEG:

- ACPI-高级配置和电源接口

- BCD 的启动配置数据

- BIOS 的基本输入/输出系统

- CSM 的兼容性支持模块

- eMMC-嵌入多媒体控制器

- ESRT – EFI 系统资源表

- GPT-GUID 分区表

- GUID-唯一全局标识

- HDD 的硬盘驱动器上

- HSTI / HSTS – 硬件安全可测试性接口 / 规范

- HVCI-虚拟机监控程序代码完整性

- IOMMU 的输入-输出内存管理单元

- [INT10](https://en.wikipedia.org/wiki/INT_10H) -BIOS 中断调用用于基本的视频显示器

- MAT/MADT – 内存 A

- MBR-主启动记录

- MOR – 内存覆盖请求

- OEM-原始设备制造商/生产

- RPMC – 重播保护单调的计数器

- SMBIOS – 系统管理的基本输入的输出系统

- SPI-串行外围接口

- TCG 的受信任计算组

- TPM – 受信任的平台模块

- 统一可扩展固件接口 （uefi)

- WEG – Windows 工程指南

- WinPE 的 Windows 预安装环境

- WinRE-Windows 恢复环境

- WSMT-Windows SMM 安全缓解措施表



