---
title: 禁用 APC
description: 禁用 APC
ms.assetid: 0578df31-1467-4bad-ba62-081d61278deb
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 禁用 Apc
- 临界区 WDK 内核
- 受保护的区域 WDK 内核
- 引发当前于 Irql
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1805e5f89e8698e632aa42393ec75d93d207aa9a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384988"
---
# <a name="disabling-apcs"></a>禁用 APC


系统提供了三种机制，用于禁用当前线程的 Apc:

-   **关键区域。** 当线程关键的区域内，不会执行其用户 Apc 和正常内核 Apc。 继续执行特殊内核 Apc。 有关这些 APC 类型的详细信息，请参阅[类型的 Apc](types-of-apcs.md)。

-   **受保护的区域。** 当线程在受保护区域内，则不执行任何其 Apc。

-   **引发当前 IRQL 到 APC\_级别或更高版本。** IRQL 同时正执行的线程&gt;= APC\_使用禁用的所有 Apc 的级别执行。

请注意，这些设置将应用于当前线程不会影响任何其他线程的行为。

某些驱动程序支持例程的调用必须使用特定种类的 Apc 禁用。 例如，获取执行资源的例程 (如[ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)) 必须与正常内核已禁用的 Apc 调用。 必须使用特定种类的 Apc 启用调用其他例程。 例如，任何依赖的 I/O 完成例程的例程 (如[ **IoVolumeDeviceToDosName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iovolumedevicetodosname)) 必须使用特殊内核 Apc 启用调用。 为每个例程的文档指定例程是否具有状态的 APC 执行任何特定限制。

驱动程序可以通过调用相应的例程来显式输入关键的或受保护区域。 有关详细信息，请参阅[临界区和受保护区域](critical-regions-and-guarded-regions.md)。 驱动程序可以显式引发 APC 为当前 IRQL\_级别通过调用[ **KeRaiseIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)。 该驱动程序必须随后通过调用降低到其原始值 IRQL [ **KeLowerIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)。 使用受保护的区域的速度快于提高和降低当前 IRQL，但是受保护的区域仅在 Windows Server 2003 和更高版本的 Windows 中可用。

以下的互斥体操作已进入或离开关键的或受保护区域或引发或降低当前 IRQL 与相同的效果：

-   隐式持有互斥体对象内的关键区域将持有者。

-   隐式持有受保护的互斥锁放置在受保护区域内的持有者。

-   隐式持有快速互斥锁引发 APC 为当前 IRQL\_级别。

有关互斥体对象的详细信息，请参阅[互斥体对象](mutex-objects.md)。 有关快速、 受保护的互斥体的详细信息，请参阅[快速互斥锁和受保护的互斥体](fast-mutexes-and-guarded-mutexes.md)。

 

 




