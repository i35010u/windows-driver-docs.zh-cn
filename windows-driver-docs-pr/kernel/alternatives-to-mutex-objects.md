---
title: 互斥对象的替代方案
description: 互斥对象的替代方案
keywords:
- 内核调度程序对象 WDK，mutex 对象
- 调度程序对象 WDK 内核，mutex 对象
- mutex 对象 WDK 内核
- 快速互斥体 WDK 内核
- 受保护的 mutex WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9692c7a5d31b09c744017f44de0b3e5c76e100
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836927"
---
# <a name="alternatives-to-mutex-objects"></a>互斥对象的替代方案


快速互斥体和受保护的互斥体可用作 mutex 对象的替换。 快速 mutex 或受保护的互斥体的获取和释放速度要快于 mutex 对象，但具有以下限制：

-   驱动程序无法使用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects) 例程等待快速或受保护的 mutex。 因此，驱动程序无法等待快速或受保护的 mutex 和调度程序对象同时等待。

-   驱动程序无法以递归方式获取快速或受保护的互斥体。 如果驱动程序尝试获取已获取的快速或受保护的互斥体，则驱动程序将死锁。 但是，可以以递归方式获取互斥体对象。

有关快速和受保护的互斥体的详细信息，请参阅 [快速互斥体和受保护的互斥体](fast-mutexes-and-guarded-mutexes.md)。

 

