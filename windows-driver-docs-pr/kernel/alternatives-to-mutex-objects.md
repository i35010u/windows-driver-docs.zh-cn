---
title: 互斥对象的替代方案
description: 互斥对象的替代方案
ms.assetid: c3b78155-426a-449d-8678-5666a7a12cbd
keywords:
- 内核调度程序对象 WDK，互斥体对象
- 调度程序对象 WDK 内核，互斥体对象
- 互斥体对象 WDK 内核
- 快速互斥体，WDK 内核
- 受保护的互斥体 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1109fc0c63923c954ac3ef43247e80a16bc72f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369955"
---
# <a name="alternatives-to-mutex-objects"></a>互斥对象的替代方案


快速互斥锁和受保护的互斥锁可替换的互斥体对象。 快速 mutex 或受保护的互斥体可以获取和释放比 mutex 对象，但它们具有以下限制：

-   驱动程序不能使用[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)或[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)例程等待快速或受保护的互斥体。 因此，驱动程序不能等待快速或受保护的互斥体和调度程序对象同时。

-   驱动程序无法获取快速或受保护的互斥体以递归方式。 如果尝试获取快速或受保护的互斥体已获得驱动程序，该驱动程序将发生死锁。 Mutex 对象，但是，可以是递归获得。

有关快速、 受保护的互斥体的详细信息，请参阅[快速互斥锁和受保护的互斥体](fast-mutexes-and-guarded-mutexes.md)。

 

 




