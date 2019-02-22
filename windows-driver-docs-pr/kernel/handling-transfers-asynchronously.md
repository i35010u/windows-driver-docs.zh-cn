---
title: 以异步方式处理传输
description: 以异步方式处理传输
ms.assetid: 84b231bd-54ff-4312-8e6c-cfc33e72b8cc
keywords:
- DispatchRead 例程
- DispatchWrite 例程
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchWrite 例程
- 调度例程 WDK 内核，DispatchRead 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
- 异步传输 WDK 内核
- 数据传输 WDK 内核异步
- 传输数据 WDK 内核，异步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5934d6193d87c05e44fdf7fed8a0609e5961650
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521179"
---
# <a name="handling-transfers-asynchronously"></a>以异步方式处理传输





除了最高级别的驱动程序的所有驱动程序处理[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写** ](https://msdn.microsoft.com/library/windows/hardware/ff550819)异步请求。 *DispatchRead*并*DispatchWrite*甚至最高级别的驱动程序中的例程不能等待较低级驱动程序，以完成处理异步读取或写入请求; 它们必须通过此类请求到低级驱动程序并返回状态\_PENDING。

同样，最低级别的设备驱动程序的*DispatchReadWrite*例程必须传输将请求传递到其他驱动程序例程来处理设备 I/O 请求并返回状态\_PENDING。

更高级别的驱动程序有时必须设置部分传输 Irp，并将它们传递到较低的驱动程序。 更高级别的驱动程序可以完成原始读/写 IRP，仅当其部分传输请求已完成的较低的驱动程序。

例如，SCSI 类驾*DispatchReadWrite*例程所需拆分超出基础 HBA 传输功能为一系列部分传输请求的大型传输请求。 在类驱动程序必须设置其部分传输 Irp 中的参数，以便 SCSI 端口/微型端口驱动程序可满足单个 DMA 操作中的每个部分传输请求。

使用 DMA 或 PIO 其他设备驱动程序可能还需要为自己拆分大型传输请求。

有关使用 DMA 和 PIO 的详细信息，请参阅[输入/输出技术](i-o-programming-techniques.md)。

 

 




