---
title: NDIS i/o 工作项
description: NDIS i/o 工作项
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- I/o 工作项 WDK NDIS
- I/o WDK 内核，NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5da84ccde12642e8eda1a7601b8525c70adf9eb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843548"
---
# <a name="ndis-io-work-items"></a>NDIS i/o 工作项





驱动程序可以将 i/o 工作项回调函数排队，以便以后执行。 NDIS 调用驱动程序指定的回调函数，其 IRQL = 被动\_级别。 这可以通过允许当前函数立即返回并使驱动程序在以后以较低的 IRQL 完成工作，从而提高系统性能。

NDIS 6.0 和更高版本为内核 i/o 工作项例程[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)和[**IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)提供包装函数。 与专用[**io\_工作**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)项结构相反，ndis 使用 **\_IO\_工作**项结构。

NDIS 6.0 驱动程序调用[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)函数来分配工作项。 NDIS 微型端口驱动程序将**NdisAllocateIoWorkItem**传递给[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的适配器句柄。 **NdisAllocateIoWorkItem**获取与句柄关联的设备对象，并将设备对象传递给[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)例程。 筛选器驱动程序在筛选器句柄中传递。

**请注意**  协议驱动程序无法使用[**NDISALLOCATEIOWORKITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem) ，因为 NDIS 不会将协议驱动程序与设备对象相关联。

 

NDIS 驱动程序调用[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)函数对工作项进行排队。 NDIS 工作项使用**CriticalWorkQueue**队列类型。

NDIS 驱动程序必须调用[**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)函数，以释放与[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)分配的工作项关联的资源。

## <a name="related-topics"></a>相关主题


[系统工作线程](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)

 

 






