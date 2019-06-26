---
title: NDIS I/O 工作项
description: NDIS I/O 工作项
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- I/O 工作项 WDK NDIS
- I/O WDK 内核 NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f66c817bde997454caf5fb1f07202c5f95afe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385516"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 工作项





驱动程序可以进行排队供以后执行 I/O 的工作项回调函数。 NDIS 调用驱动程序指定的回调函数在 IRQL = 被动\_级别。 这要立即返回的当前函数和驱动程序来执行较低的 IRQL 在更高版本工作，从而提高系统性能。

NDIS 6.0 及更高版本提供包装器函数的内核 I/O 的工作项例程[ **IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)， [ **IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)，并[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)。 而不是私有[ **IO\_工作项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，NDIS 使用专用**NDIS\_IO\_工作项**结构。

NDIS 6.0 驱动程序调用[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)函数以分配工作项。 NDIS 微型端口驱动程序通过**NdisAllocateIoWorkItem**适配器处理传递给该 NDIS [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 **NdisAllocateIoWorkItem**获取与句柄关联的设备对象并将传递到的设备对象[ **IoAllocateWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)例程。 筛选器驱动程序传入筛选器句柄。

**请注意**  协议驱动程序不能使用[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)因为 NDIS 不会将设备对象与关联协议驱动程序。

 

NDIS 驱动程序调用[ **NdisQueueIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisqueueioworkitem)函数工作项排队。 NDIS 工作项使用**CriticalWorkQueue**队列类型。

NDIS 驱动程序必须调用[ **NdisFreeIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreeioworkitem)函数来释放与工作相关联的资源项[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)分配。

## <a name="related-topics"></a>相关主题


[系统工作线程数](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)

 

 






