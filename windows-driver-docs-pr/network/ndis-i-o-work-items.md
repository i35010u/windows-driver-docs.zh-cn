---
title: NDIS I/O 工作项
description: NDIS I/O 工作项
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- I/O 工作项 WDK NDIS
- I/O WDK 内核 NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e9e4d95abf4be742857812787ea3e3c0afcb1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392914"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 工作项





驱动程序可以进行排队供以后执行 I/O 的工作项回调函数。 NDIS 调用驱动程序指定的回调函数在 IRQL = 被动\_级别。 这要立即返回的当前函数和驱动程序来执行较低的 IRQL 在更高版本工作，从而提高系统性能。

NDIS 6.0 及更高版本提供包装器函数的内核 I/O 的工作项例程[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)， [ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)，并[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)。 而不是私有[ **IO\_工作项**](https://msdn.microsoft.com/library/windows/hardware/ff550679)结构，NDIS 使用专用**NDIS\_IO\_工作项**结构。

NDIS 6.0 驱动程序调用[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)函数以分配工作项。 NDIS 微型端口驱动程序通过**NdisAllocateIoWorkItem**适配器处理传递给该 NDIS [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 **NdisAllocateIoWorkItem**获取与句柄关联的设备对象并将传递到的设备对象[ **IoAllocateWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff548276)例程。 筛选器驱动程序传入筛选器句柄。

**请注意**  协议驱动程序不能使用[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)因为 NDIS 不会将设备对象与关联协议驱动程序。

 

NDIS 驱动程序调用[ **NdisQueueIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff563775)函数工作项排队。 NDIS 工作项使用**CriticalWorkQueue**队列类型。

NDIS 驱动程序必须调用[ **NdisFreeIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561855)函数来释放与工作相关联的资源项[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)分配。

## <a name="related-topics"></a>相关主题


[系统工作线程数](https://msdn.microsoft.com/library/windows/hardware/ff564587)

 

 






