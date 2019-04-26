---
title: 处理 NIC 意外删除 (Windows Vista)
description: 处理 NIC 意外删除 (Windows Vista)
ms.assetid: 940E6109-0A4C-4F4C-8201-F28BB789D7AE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7f596715d92f2540bb6c11cac042f4aa32189bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327649"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-vista"></a>处理 NIC 意外删除 (Windows Vista)





以下步骤介绍 NDIS 参与 Windows Vista 和 Windows Server 2008 中的 NIC 被意外删除的方式：

1.  即插即用 manager 问题[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)设备堆栈对 nic 的请求

2.  当 NDIS 接收此 IRP 时，它将调用[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)附加到的 NIC 驱动程序堆栈中的最小筛选器驱动程序的函数。 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 执行此步骤中，仅对播发条目的筛选器驱动程序，为点[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。 筛选器驱动程序播发此入口点时它将调用[ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)函数。

     

3.  对调用的上下文中其[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数，筛选器驱动程序必须调用[ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)转发**NetEventQueryRemoveDevice**事件传送至驱动程序堆栈中的下一个筛选器驱动程序。 这将导致调用该筛选器驱动程序的 NDIS *FilterNetPnPEvent*函数的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 仅对播发的入口点的驱动程序堆栈中的下一个筛选器驱动程序执行此步骤[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)函数。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中最高的筛选器驱动程序已转发**NetEventQueryRemoveDevice。** 事件。

    当发生这种情况，将调用 NDIS [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数绑定到 NIC 的所有协议驱动程序 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

5.  如果已成功初始化微型端口驱动程序，调用 NDIS [ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)函数中的事件代码为**NdisDevicePnPEventSurpriseRemoved**. 微型端口驱动程序应注意，以物理方式删除设备。 如果微型端口驱动程序是 NDIS WDM 驱动程序，它应取消任何挂起的 Irp，它向下发送到基础总线驱动程序。 如果未成功初始化微型端口驱动程序，继续进行处理。

6.  NDIS 发送 IRP\_MN\_惊讶\_对堆栈中的下一步下一个设备对象的删除请求。 后接收返回的 IRP\_MN\_惊讶\_从下一步低设备的删除请求对象在堆栈中 NDIS 完成 IRP\_MN\_惊讶\_删除请求。

7.  即插即用 manager 问题[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求删除 NIC 的软件表示 （设备对象等）

8.  NDIS 将执行以下步骤：

    1.  它将暂停所有协议驱动程序绑定到 nic。

    2.  附加到 NIC 的所有筛选器驱动程序，它将暂停

    3.  微型端口驱动程序的 NIC，它将暂停

    4.  它将调用[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数绑定到 NIC 的所有协议驱动程序

    5.  它将调用[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)附加到 NIC 的所有筛选器模块的函数

9.  NDIS 之间的绑定，并且所有的协议和筛选器驱动程序从 NIC 中分离后，调用微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。 NDIS 集*HaltAction*的参数*MiniportHaltEx*到**NdisHaltDeviceSurpriseRemoved**。

10. NDIS 发送 IRP\_MN\_删除\_设备请求到堆栈中较低的下一个设备对象。

11. 当 NDIS 收到已完成的 IRP\_MN\_删除\_从下一个较低的设备的设备请求对象在堆栈中 NDIS 销毁功能的设备对象 (FDO) 创建的 nic。

 

 





