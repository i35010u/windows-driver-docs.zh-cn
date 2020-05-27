---
title: Bug 检查 0x1D0 ACPI_FIRMWARE_WATCHDOG_TIMEOUT
description: ACPI_FIRMWARE_WATCHDOG_TIMEOUT bug 检查的值为0x000001D0。
keywords:
- Bug 检查 0x1D0 ACPI_FIRMWARE_WATCHDOG_TIMEOUT
- ACPI_FIRMWARE_WATCHDOG_TIMEOUT
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- ACPI_FIRMWARE_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2465fd5baade86ab0274a0861df9293fa8fe195
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851982"
---
# <a name="bug-check-0x1d0-acpi_firmware_watchdog_timeout"></a>Bug 检查0x1D0： ACPI \_ 固件 \_ 监视器 \_ 超时 


> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


ACPI_FIRMWARE_WATCHDOG_TIMEOUT bug 检查的值为0x000001D0。 

ACPI 驱动程序无法在预期的分配时间内完成操作。

## <a name="acpi_firmware_watchdog_timeout-parameters"></a>ACPI \_ 固件 \_ 监视器 \_ 超时参数

以下参数显示在蓝色屏幕上。

参数 | 说明 
|---------|--------------|
1 | 指向 AMLI 上下文的指针
2 | 指向 Aml 上下文的 Unicode 名称的指针
3 | 指向 ACPI 设备扩展的指针。
4 | 指向 ACPI 会审块的指针。





