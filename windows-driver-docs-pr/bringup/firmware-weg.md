---
title: 固件 Windows 工程指南 (WEG)
description: 固件 Windows 工程指南 (WEG) 提供了在实施与系统固件相关的最佳做法时需遵循的路线图。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6a8ede9c66240420868b1396f9a2bda1aeedde5
ms.sourcegitcommit: 5cbfbfe1e8fa18f3c656dabbeb7ee88b5dc065c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414824"
---
# <a name="firmware-windows-engineering-guide-weg"></a>固件 Windows 工程指南 (WEG)

固件 Windows 工程指南 (WEG) 提供了在实施与系统固件相关的最佳做法时需遵循的路线图。


## <a name="in-this-section"></a>在本节中

[UEFI 安全性](uefi-security.md)

[固件更新](firmware-update.md)

[SMBIOS](smbios.md)

[HTTPS](https-boot.md)

[固件中的 Wi-Fi 支持](wi-fi-support-in-firmware.md)

[从旧的 MBR 磁盘切换到 Windows 10 的 GPT 磁盘](switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10.md)

[固件 WEG 常见问题解答](frequently-asked-questions.md)

[为 Windows 7 及 Windows 10 的更高版本的更新配置系统固件](configure-system-firmware-for-windows-7-and-later-update-for-windows-10.md)

[用于在本地查询 SMBIOS 的示例 PowerShell 脚本](sample-powershell-script-to-query-smbios-locally.md)

                                           





## <a name="firmware-weg-terminology"></a>固件 WEG 术语

在固件 WEG 中使用以下术语：

- ACPI-高级配置和电源接口

- ACHI-高级配置主机接口

- BCD-引导配置数据

- BIOS-基本输入/输出系统

- CSM 兼容性支持模块

- EFI 可扩展的 Fireware 接口 

- eMMC-嵌入的多介质控制器

- ESRT – EFI 系统资源表

- GPT - GUID 分区表

- GUID –全局唯一标识

- 硬盘-硬盘驱动器

- HSTI/HSTS-硬件安全可测试性接口/规范

- 要求 HVCI-虚拟机监控程序代码完整性

- IOMMU –输入-输出内存管理单元

- [INT10](https://en.wikipedia.org/wiki/INT_10H) -用于视频基本显示的 BIOS 中断调用

- "材料-内存属性" 表

- MADT-多个 APIC 说明表

- MBR-主启动记录

- MOR –内存覆盖请求

- NVRAM-非易失性随机存取内存

- OEM-原始设备制造商/生产

- PCIe-外围组件互连 express

- RPMC-重播 Protected 单调计数器

- SMBIOS –系统管理基本输入输出系统

- SPI - 串行外设接口

- SSD-固态驱动器 

- TCG-受信任的计算组

- TPM-受信任的平台模块

- UEFI-统一可扩展固件接口

- WAET-Windows ACPI EmulatedDevices 表

- WDDM-Windows 显示驱动程序模型

- WEG – Windows 工程指南

- WHQL-Windows 硬件质量实验室

- WinPE-Windows 预安装环境

- WinRE-Windows 恢复环境

- WPBT-Windows 平台二进制表

- WSMT-Windows SMM 安全缓解表



