---
title: 以异步方式处理传输
description: 以异步方式处理传输
keywords:
- DispatchRead 例程
- DispatchWrite 例程
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchWrite 例程
- 调度例程 WDK 内核，DispatchRead 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
- 异步传输 WDK 内核
- 数据传输 WDK 内核，异步
- 传输数据 WDK 内核，异步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ec1f4f1762dfc7d6217e7ffba57ab9d657106b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836925"
---
# <a name="handling-transfers-asynchronously"></a>以异步方式处理传输





除最高层驱动程序外，所有驱动程序都以异步方式处理 [**IRP \_ mj \_ 读取**](./irp-mj-read.md) 和 [**irp \_ mj \_ 写入**](./irp-mj-write.md) 请求。 即使是最高级别的驱动程序中的 *DispatchRead* 和 *DispatchWrite* 例程，也无法等待较低级别的驱动程序完成对异步读取或写入请求的处理;它们必须将此类请求传递到更低的驱动程序，并返回 "挂起" 状态 \_ 。

同样，最低级别设备驱动程序的 *DispatchReadWrite* 例程必须将传输请求传递给处理设备 i/o 请求的其他驱动程序例程，然后返回状态 "挂起" \_ 。

较高级别的驱动程序有时必须设置部分传输的 Irp，并将其传递到较低的驱动程序。 只有当驱动程序的部分传输请求已经完成后，较低级别的驱动程序才能完成原始的读/写 IRP。

例如，SCSI 类驱动程序的 *DispatchReadWrite* 例程需要将超过底层 HBA 传输功能的大型传输请求拆分为一组部分传输请求。 类驱动程序必须在其部分传输子请求中设置参数，以便 SCSI 端口/微型端口驱动程序可以在单个 DMA 操作中满足每个部分传输请求。

使用 DMA 或 PIO 的其他设备驱动程序还可能需要为其单独拆分大型传输请求。

有关使用 DMA 和 PIO 的详细信息，请参阅 [输入/输出技术](i-o-programming-techniques.md)。

 

