---
title: 启动驱动程序堆栈
description: 启动驱动程序堆栈
ms.assetid: 316de69e-38e8-4ac6-83c5-5d13090ee6d5
keywords:
- 驱动程序堆栈 WDK 网络启动
- 启动驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d75c5675fc16e9bcbe390538346cd5e0aa8e71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377565"
---
# <a name="starting-a-driver-stack"></a>启动驱动程序堆栈





系统检测到网络设备后，在系统启动设备的 NDIS 驱动程序堆栈。 设备可以是虚拟设备或物理设备。 在任一情况下，驱动程序堆栈开始操作继续进行，如下所示：

1.  在系统加载和初始化驱动程序，如果它们不是已加载。

    它不会加载任何特定顺序中的驱动程序。

2.  系统调用每个驱动程序**DriverEntry**函数。

    之后**DriverEntry**返回：

    -   设备的微型端口适配器处于暂停状态。
    -   筛选器模块都处于已分离的状态。
    -   协议绑定处于未绑定状态。

3.  系统请求 NDIS 启动微型端口适配器。

    若要初始化的微型端口适配器，NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 如果*MiniportInitializeEx*是成功，微型端口适配器进入暂停状态。

4.  NDIS 将附加的筛选器模块，开头的模块的最接近的微型端口驱动程序和驱动程序堆栈的顶部的进展情况。

    若要请求驱动程序将筛选器模块附加到驱动程序堆栈，NDIS 调用筛选器驱动程序[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数。 如果每个附加操作成功，筛选器模块将进入暂停状态。

5.  NDIS 基础的所有驱动程序都处于已暂停状态后，调用协议驱动程序[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

    然后协议驱动程序绑定将进入打开状态。 协议驱动程序调用[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)函数打开的微型端口适配器绑定。

6.  NDIS 绑定分配所需的资源，并调用协议驱动程序[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)函数。

    该绑定将进入暂停状态。

7.  若要完成绑定操作，协议驱动程序调用[ **NdisCompleteBindAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletebindadapterex)函数。

8.  NDIS 驱动程序堆栈，重新启动。 有关重新启动驱动程序堆栈的详细信息，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





