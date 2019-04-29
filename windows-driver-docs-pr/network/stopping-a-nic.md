---
title: 停止 NIC
description: 停止 NIC
ms.assetid: 033b45bd-fbe9-4a40-84e6-b9447370b17f
keywords:
- Nic WDK 网络停止
- 网络接口卡 WDK 网络停止
- 即插即用 WDK NDIS 微型端口，停止 NIC
- 正在停止 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8959b978c59e52ad6e4b28042c186b1a23e730ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366373"
---
# <a name="stopping-a-nic"></a>停止 NIC





PnP 管理器停止 NIC，以便它可以重新配置或重新平衡它分配给 NIC 的硬件资源 以下步骤介绍如何 NDIS 参与 NIC 停止：

1.  即插即用 manager 问题[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)请求。

2.  当 NDIS 接收此 IRP 时，它将调用[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)附加到的 NIC 驱动程序堆栈中的最小筛选器驱动程序的函数。 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 执行此步骤中，仅对播发条目的筛选器驱动程序，为点[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。 筛选器驱动程序将公布此入口点时它将调用[ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)函数。

     

3.  对调用的上下文中其[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数，筛选器驱动程序必须调用[ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)转发**NetEventQueryRemoveDevice**事件传送至驱动程序堆栈中的下一个筛选器驱动程序。 这将导致调用该筛选器驱动程序的 NDIS *FilterNetPnPEvent*函数的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 仅对播发的入口点的驱动程序堆栈中的下一个筛选器驱动程序执行此步骤[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中最高的筛选器驱动程序已转发**NetEventQueryRemoveDevice**事件。

    当发生这种情况，将调用 NDIS [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数绑定到 NIC 的所有协议驱动程序 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

5.  如果协议驱动程序失败**NetEventQueryRemoveDevice**通过返回失败代码从事件*ProtocolNetPnPEvent*，NDIS 或 PnP 管理器可能会忽略错误并随之成功IRP\_MN\_查询\_停止\_设备的请求。 协议驱动程序因此，必须准备好处理删除的 NIC，即使协议驱动程序失败**NetEventQueryRemoveDevice**事件。

6.  即插即用 manager 问题[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求停用设备或[ **IRP\_MN\_取消\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550826)取消挂起的停止请求。

7.  如果 PnP 管理器将发出 IRP\_MN\_取消\_停止\_设备请求、 NDIS 调用[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)的最小的函数附加到的 NIC 驱动程序堆栈中的筛选器驱动程序。 NDIS 此调用中指定的事件代码**NetEventCancelRemoveDevice**。

    **请注意**  NDIS 执行此步骤中，仅对播发条目的筛选器驱动程序，为点[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。

     

8.  对调用的上下文中其[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数，筛选器驱动程序必须调用[ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)转发**NetEventCancelRemoveDevice**事件传送至驱动程序堆栈中的下一个筛选器驱动程序。 这将导致调用该筛选器驱动程序的 NDIS *FilterNetPnPEvent*函数的事件代码**NetEventCancelRemoveDevice**。

    **请注意**  NDIS 仅对播发的入口点的驱动程序堆栈中的下一个筛选器驱动程序执行此步骤[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。

     

9.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中最高的筛选器驱动程序已转发**NetEventCancelRemoveDevice**事件。

    当发生这种情况，将调用 NDIS [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数绑定到 NIC 的所有协议驱动程序 NDIS 此调用中指定的事件代码**NetEventCancelRemoveDevice**。

10. 如果 PnP 管理器将发出 IRP\_MN\_停止\_设备请求，NDIS 会执行以下步骤：

    1.  它将暂停所有协议驱动程序绑定到 nic。

    2.  附加到 NIC 的所有筛选器驱动程序，它将暂停

    3.  微型端口驱动程序的 NIC，它将暂停

    4.  它将调用[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数绑定到 NIC 的所有协议驱动程序

    5.  它将调用[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)附加到 NIC 的所有筛选器模块的函数

11. NDIS 之间的绑定，并且所有的协议和筛选器驱动程序从 NIC 中分离后，调用微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。 NDIS 集*HaltAction*的参数*MiniportHaltEx*到**NdisHaltDeviceStopped**。

12. 当处理 IRP\_MN\_停止\_设备请求，NDIS 不会销毁它针对 NIC 创建的功能的设备对象 (FDO) 时*AddDevice*调用例程。 NDIS 销毁设备对象在接收后才[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738) nic 的请求

    如果 PnP 管理器将发出 IRP\_MN\_启动\_重新启动的 NIC，NDIS 设备将重用先前创建的 NIC FDO NDIS 然后重新启动的 nic。 此过程的详细信息，请参阅[启动 NIC](starting-a-nic.md)。

 

 





