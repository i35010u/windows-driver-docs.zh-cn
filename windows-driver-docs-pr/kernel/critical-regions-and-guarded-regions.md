---
title: 关键区域和受保护区域
description: 关键区域和受保护区域
ms.assetid: 3781498a-45e9-4f24-8fd2-830eed61298c
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 临界区 WDK 内核
- 受保护的区域 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2014b59cec69372fb111171f9fd6e60fd1ca84b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575180"
---
# <a name="critical-regions-and-guarded-regions"></a>关键区域和受保护区域


中的线程*临界区*执行与用户 Apc 和禁用的普通内核 Apc。 内部线程*受保护的区域*运行，并禁用所有 Apc。

### <a name="critical-regions"></a>临界区

驱动程序可以进入和退出临界区，如下所示：

-   调用[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)输入关键区域。

-   调用[ **KeLeaveCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552964)退出临界区。

每次调用**KeEnterCriticalRegion**必须具有匹配调用**KeLeaveCriticalRegion**。

### <a name="guarded-regions"></a>受保护的区域

驱动程序可以进入和退出受保护的区域，如下所示：

-   调用[ **KeEnterGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552028)输入受保护的区域。

-   调用[ **KeLeaveGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552967)保留受保护的区域。

每次调用**KeEnterGuardedRegion**必须具有匹配调用**KeLeaveGuardedRegion**。

开发用于 Windows Server 2003 和更高版本的 Windows 驱动程序可以使用受保护的区域禁用特殊内核 Apc。 驱动程序开发的早期版本的操作系统可以通过引发 APC 为当前 IRQL 禁用特殊内核 Apc\_级别通过调用[ **KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079)。 使用[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)降低当前 IRQL 到以前的值。

 

 




