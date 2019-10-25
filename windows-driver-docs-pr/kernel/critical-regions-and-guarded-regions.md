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
ms.openlocfilehash: bf81928dd90ff25c9b8279505929c80032447d24
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836972"
---
# <a name="critical-regions-and-guarded-regions"></a>关键区域和受保护区域


*关键区域*内的线程在用户 apc 和正常内核 apc 处于禁用状态时执行。 *受保护区域*中的线程将运行，并禁用所有 apc。

### <a name="critical-regions"></a>关键区域

驱动程序可以按如下所示进入和退出关键区域：

-   调用[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)进入关键区域。

-   调用[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)退出关键区域。

对**KeEnterCriticalRegion**的每次调用都必须具有对**KeLeaveCriticalRegion**的匹配调用。

### <a name="guarded-regions"></a>受保护区域

驱动程序可以按如下所示进入和退出受保护的区域：

-   调用[**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)输入受保护的区域。

-   调用[**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)以离开受保护的区域。

对**KeEnterGuardedRegion**的每次调用都必须具有对**KeLeaveGuardedRegion**的匹配调用。

为 Windows Server 2003 和更高版本的 Windows 开发的驱动程序可以使用受保护的区域来禁用特殊内核 Apc。 为较早版本的操作系统开发的驱动程序可以通过调用[**KeRaiseIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)将当前的 IRQL 提升为 APC\_级别来禁用特殊内核 apc。 使用[**KeLowerIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)将当前的 IRQL 降低到以前的值。

 

 




