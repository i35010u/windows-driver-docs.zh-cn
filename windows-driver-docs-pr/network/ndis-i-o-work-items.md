---
title: NDIS I/O 工作项
description: NDIS I/O 工作项
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- I/o 工作项 WDK NDIS
- I/o WDK 内核，NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c33c27a49b5ff30c15d3c6bf283bb348a7a5d9b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212161"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 工作项





驱动程序可以将 i/o 工作项回调函数排队，以便以后执行。 NDIS 在 IRQL = 被动级别调用驱动程序指定的回调函数 \_ 。 这可以通过允许当前函数立即返回并使驱动程序在以后以较低的 IRQL 完成工作，从而提高系统性能。

NDIS 6.0 和更高版本为内核 i/o 工作项例程 [**IoAllocateWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**IoFreeWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)和 [**IoQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)提供包装函数。 NDIS 使用私有的**ndis \_ io \_ 工作**项结构，而不是专用[**io \_ 工作**](../kernel/eprocess.md)项结构。

NDIS 6.0 驱动程序调用 [**NdisAllocateIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem) 函数来分配工作项。 NDIS 微型端口驱动程序将 **NdisAllocateIoWorkItem** 传递给 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数的适配器句柄。 **NdisAllocateIoWorkItem** 获取与句柄关联的设备对象，并将设备对象传递给 [**IoAllocateWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem) 例程。 筛选器驱动程序在筛选器句柄中传递。

**注意**   协议驱动程序无法使用[**NdisAllocateIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem) ，因为 NDIS 不会将协议驱动程序与设备对象相关联。

 

NDIS 驱动程序调用 [**NdisQueueIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem) 函数对工作项进行排队。 NDIS 工作项使用 **CriticalWorkQueue** 队列类型。

NDIS 驱动程序必须调用 [**NdisFreeIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem) 函数，以释放与 [**NdisAllocateIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem) 分配的工作项关联的资源。

## <a name="related-topics"></a>相关主题


[系统工作线程](../kernel/system-worker-threads.md)

 

