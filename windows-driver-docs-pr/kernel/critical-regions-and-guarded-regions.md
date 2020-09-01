---
title: 关键区域和受保护区域
description: 关键区域和受保护区域
ms.assetid: 3781498a-45e9-4f24-8fd2-830eed61298c
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 关键区域 WDK 内核
- 受保护区域 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0f32cb0aabb7f543af34a5acf2908e86f7d17bb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191967"
---
# <a name="critical-regions-and-guarded-regions"></a>关键区域和受保护区域


*关键区域*内的线程在用户 apc 和正常内核 apc 处于禁用状态时执行。 *受保护区域*中的线程将运行，并禁用所有 apc。

### <a name="critical-regions"></a>关键区域

驱动程序可以按如下所示进入和退出关键区域：

-   调用 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 进入关键区域。

-   调用 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 退出关键区域。

对 **KeEnterCriticalRegion** 的每次调用都必须具有对 **KeLeaveCriticalRegion**的匹配调用。

### <a name="guarded-regions"></a>受保护区域

驱动程序可以按如下所示进入和退出受保护的区域：

-   调用 [**KeEnterGuardedRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion) 输入受保护的区域。

-   调用 [**KeLeaveGuardedRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion) 以离开受保护的区域。

对 **KeEnterGuardedRegion** 的每次调用都必须具有对 **KeLeaveGuardedRegion**的匹配调用。

为 Windows Server 2003 和更高版本的 Windows 开发的驱动程序可以使用受保护的区域来禁用特殊内核 Apc。 为早期操作系统开发的驱动程序可以通过调用 KeRaiseIrql，将当前的 IRQL 提升到 APC 级别来禁用特殊内核 Apc \_ 。 [**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql) 使用 [**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) 将当前的 IRQL 降低到以前的值。

 

