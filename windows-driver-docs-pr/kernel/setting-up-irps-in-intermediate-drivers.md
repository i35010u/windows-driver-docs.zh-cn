---
title: 在中间驱动程序中设置 IRP
description: 在中间驱动程序中设置 IRP
ms.assetid: 0d04a951-a68e-4fa1-bdc6-dd92ec49deae
keywords:
- 可移动媒体 WDK 内核，中间层驱动程序 Irp
- 中间驱动程序 Irp WDK 可移动媒体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc848103b57c6c6b52c96c89c88c452004c5375e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367866"
---
# <a name="setting-up-irps-in-intermediate-drivers"></a>在中间驱动程序中设置 IRP





分层文件系统驱动程序和可移动介质设备驱动程序之间的任何中间驱动程序必须设置 Irp 中的下一步低级驱动程序的 I/O 堆栈位置。 从传入[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)， [ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)，和[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求时，中间驱动程序必须将其自己的 I/O 堆栈位置复制**标志**到下一步低级驱动程序的 I/O 堆栈位置时设置较低的驱动程序的 I/O 堆栈位置。

如果中间驱动程序为较低级别可移动媒体驱动程序分配新 Irp，它必须按如下所示设置这些 Irp:

-   对于传输请求，它必须设置的线程上下文中每个驱动程序分配的 IRP 处的值从**Tail.Overlay.Thread**中原始 IRP。

-   有关**IRP\_MJ\_读取**， **IRP\_MJ\_编写**，并**IRP\_MJ\_设备\_控制**请求时，它必须将复制的 I/O 堆栈位置**标志**从原始 IRP 到每个驱动程序分配的 IRP。

否则为文件系统可以既不维护的缓存的文件数据的完整性也不会使用户，会提示您重新装载保留打开的文件的介质。

 

 




