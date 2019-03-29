---
title: 物理内存量的更改
description: 物理内存量的更改
ms.assetid: 5ab1d598-e702-4fc7-aab4-7b7726c3a552
keywords:
- 动态硬件分区 WDK，物理内存
- 硬件分区 WDK 动态的物理内存
- 分区 WDK 动态硬件，物理内存
- 物理内存 WDK 动态硬件分区
- 内存 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b5e566b3456886913988461e9469b3ed6e5af45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565164"
---
# <a name="changes-to-the-amount-of-physical-memory"></a>物理内存量的更改


动态可分区服务器上，可以在任何时间添加到硬件分区的内存模块。 因此，不进行任何假设存在硬件分区中的物理内存量。

如果设备驱动程序硬件分区中使用的物理内存量，以确定它在分配的内存缓冲区的大小，以便它将正常工作的动态可分区服务器上时动态添加，则必须更新该驱动程序内存与硬件分区。

如果设备驱动程序的物理内存量更改的影响，它必须与操作系统内存添加到硬件分区时收到通知注册。 当通知的设备驱动程序时，它可以响应根据需要以确保安全和最佳操作。 有关设备驱动程序如何可以注册其自身与操作系统的详细信息，请参阅[驱动程序通知](driver-notification.md)。

**请注意**  从 Windows Server 2008 开始，使用的分页和非分页系统内存池的大小后不要更改操作系统启动。 因此，如果将内存添加到硬件分区，在这些系统的内存池中的内存量不会更改。

 

 

 




