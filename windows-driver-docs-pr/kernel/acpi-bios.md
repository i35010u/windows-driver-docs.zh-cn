---
title: ACPI BIOS
description: ACPI BIOS
ms.assetid: 787e82ed-e58c-461f-abb6-71ed6cba411c
keywords:
- ACPI BIOS WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e62f38b0068eeb2a52e5e2fc176295a07e0461
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363459"
---
# <a name="acpi-bios"></a>ACPI BIOS





Microsoft Windows 操作系统支持的集成的电源管理功能都可仅在具有高级配置和电源接口 (ACPI) BIOS 的计算机上。

Windows Server 2003、 Windows XP 和 Windows 2000 要求 ACPI BIOS 日期 1999 年 1 月 1 日或更高版本。 但是，如果这些 Windows 版本之一确定此类 BIOS 已知展现出 ACPI 问题，加载程序禁用 ACPI，并改为使用高级电源管理 (APM)。 操作系统从 Windows Vista 开始，支持仅使用日期 1999 年 1 月 1 日或更高版本符合 ACPI BIOS 的计算机。

设备管理器显示的单台计算机是否支持 ACPI。 检查驱动程序信息**计算机**设备类别。

ACPI 的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)。

