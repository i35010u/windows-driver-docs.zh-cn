---
title: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
description: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e84a589aa2fe32348f2dcfc9bbc19dcb192692cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838779"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose 和 DispatchCreateClose 例程





驱动程序的 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) irp，其中的 i/o 函数代码为 [**IRP \_ mj \_**](./irp-mj-create.md) ，并分别创建和 [**IRP \_ mj \_ CLOSE**](./irp-mj-close.md)。 此外，组合的 [*DispatchCreateClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程还可以处理这两个 i/o 函数代码的 irp。

Create 请求可以从用户模式子系统的尝试获取表示设备的句柄的文件对象的句柄， (可能代表应用程序或子系统级驱动程序) 或者在更高级别的驱动程序中调用 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 或 [**IoAttachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)。

互惠关闭请求源自与驱动程序的设备对象关联的文件对象句柄的用户模式子系统。

其中每个请求都是同步的。

 

