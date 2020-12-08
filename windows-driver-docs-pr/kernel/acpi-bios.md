---
title: ACPI BIOS
description: ACPI BIOS
keywords:
- ACPI BIOS WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a195904a22d9a95db196bf787206455cc0c9ffc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832303"
---
# <a name="acpi-bios"></a>ACPI BIOS





Microsoft Windows 操作系统支持的集成电源管理功能仅在具有高级配置和电源接口 (ACPI) BIOS 的计算机上可用。

Windows Server 2003、Windows XP 和 Windows 2000 要求 ACPI BIOS 日期为年1月 1 1999 日。 但是，如果这些 Windows 版本之一确定此类 BIOS 出现 ACPI 问题，则加载程序将禁用 ACPI，并改为使用高级电源管理 (APM) 。 从 Windows Vista 开始，操作系统仅支持具有1999年1月1日或更高版本的 ACPI 兼容 BIOS 的计算机。

设备管理器显示单个计算机是否支持 ACPI。 查看 **计算机** 设备类别的驱动程序信息。

有关 ACPI 的详细信息，请参阅 [acpi 5.0 规范](https://uefi.org/specifications)。

