---
title: 注册 WDM 下边缘的微型端口驱动程序函数
description: 注册 WDM 下边缘的微型端口驱动程序函数
ms.assetid: 68048d36-d57c-4ad9-a15e-92b1d7866d4a
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，注册函数
- NDIS-WDM 微型端口驱动程序 WDK 网络，入口点函数
- NDIS 微型端口驱动程序的下边缘 WDK 网络，入口点函数
- WDM 低边缘 WDK 网络，入口点函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e4141766977cabce2e774f919fc022b1ed53028
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211991"
---
# <a name="registering-miniport-driver-functions-for-wdm-lower-edge"></a>注册 WDM 下边缘的微型端口驱动程序函数





具有 WDM 下边缘的微型端口驱动程序必须调用其**DriverEntry**例程中的[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数，才能向 NDIS 库注册某些入口点函数。 这些入口点函数组成微型端口驱动程序的上边缘，在 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)中进行了介绍。 但是，如果设置某些入口点函数，则无需使用 WDM 低边缘的微型端口驱动程序。 例如，以下入口点函数未设置，原因如下：

-   [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)、 [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)、 [*MiniportEnableInterruptEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_interrupt)和 [*MiniportDisableInterruptEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_interrupt)

    由于微型端口驱动程序不会从物理网络接口卡 (NIC) 接收中断，因此不需要这些入口点例程。 当数据包到达要用于微型端口驱动程序的总线时，特定总线的驱动程序将接收中断。 然后，总线驱动程序通知微型端口驱动程序。

-   [*MiniportSharedMemoryAllocateComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_allocate_shared_mem_complete)

    由于微型端口驱动程序不分配共享内存，因此未指定完成入口点例程。

-   [*MiniportCheckForHangEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)

    微型端口驱动程序可以依赖 NDIS 来确定其微型端口实例是否已停止响应，这是因为发送和请求超时，因此通常不需要此例程。

 

