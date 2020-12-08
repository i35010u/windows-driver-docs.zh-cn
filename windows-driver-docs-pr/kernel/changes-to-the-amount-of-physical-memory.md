---
title: 物理内存量的更改
description: 物理内存量的更改
keywords:
- 动态硬件分区 WDK，物理内存
- 硬件分区 WDK 动态，物理内存
- 将 WDK 动态硬件分区、物理内存分区
- 物理内存 WDK 动态硬件分区
- 内存 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce48d2fbde7c8214c80bef88243983fd0feb5d8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828557"
---
# <a name="changes-to-the-amount-of-physical-memory"></a>物理内存量的更改


在动态分区的服务器上，可以随时将内存模块添加到硬件分区。 因此，请不要对硬件分区中存在的物理内存量作出任何假设。

如果设备驱动程序使用硬件分区中的物理内存量来确定所分配的内存缓冲区的大小，则必须更新驱动程序，以便在将内存动态添加到硬件分区时，它将在动态分区服务器上正常运行。

如果设备驱动程序受物理内存量的更改的影响，则它必须向操作系统注册自己，以便在将内存添加到硬件分区时收到通知。 当设备驱动程序得到通知时，它可以根据需要进行响应，以确保安全和最佳操作。 有关设备驱动程序如何向操作系统注册自身的详细信息，请参阅 [驱动程序通知](introduction-to-driver-notification.md)。

**注意**  从 Windows Server 2008 开始，分页和未分页的系统内存池的大小在操作系统启动后不会更改。 因此，如果将内存添加到硬件分区，则这些系统内存池中的内存量不会改变。

 

 

 




