---
title: 启动驱动程序堆栈
description: 启动驱动程序堆栈
keywords:
- 驱动程序堆栈 WDK 网络，开始
- 启动驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f29de431354b886bb998537ff5cf98d1f71d2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801283"
---
# <a name="starting-a-driver-stack"></a>启动驱动程序堆栈





系统检测到网络设备后，系统会启动设备的 NDIS 驱动程序堆栈。 设备可以是虚拟设备或物理设备。 在任一情况下，驱动程序堆栈启动操作都会继续执行，如下所示：

1.  系统加载并初始化驱动程序（如果尚未加载）。

    它不会以任何特定顺序加载驱动程序。

2.  系统调用每个驱动程序的 **DriverEntry** 函数。

    **DriverEntry** 返回后：

    -   设备的微型端口适配器处于暂停状态。
    -   筛选器模块处于分离状态。
    -   协议绑定处于未绑定状态。

3.  系统请求 NDIS 启动微型端口适配器。

    为了初始化微型端口适配器，NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数。 如果 *MiniportInitializeEx* 成功，微型端口适配器将进入暂停状态。

4.  NDIS 附加筛选器模块，从与微型端口驱动程序最接近的模块开始，到驱动程序堆栈的顶部。

    为了请求驱动程序将筛选器模块附加到驱动程序堆栈，NDIS 调用筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数。 如果每个附加操作成功，筛选器模块将进入暂停状态。

5.  所有底层驱动程序都处于暂停状态之后，NDIS 将调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数。

    然后，协议驱动程序绑定进入 "正在打开" 状态。 协议驱动程序调用 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 函数来打开具有微型端口适配器的绑定。

6.  NDIS 为绑定分配所需的资源，并调用协议驱动程序的 [*ProtocolOpenAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex) 函数。

    绑定进入暂停状态。

7.  若要完成绑定操作，协议驱动程序将调用 [**NdisCompleteBindAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletebindadapterex) 函数。

8.  NDIS 重启驱动程序堆栈。 有关重新启动驱动程序堆栈的详细信息，请参阅 [重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

