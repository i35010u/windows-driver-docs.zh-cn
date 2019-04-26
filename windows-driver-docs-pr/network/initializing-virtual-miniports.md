---
title: 初始化虚拟微型端口
description: 初始化虚拟微型端口
ms.assetid: b712fe29-fd56-4abd-bab6-e335350a20c2
keywords:
- 打开 WDK 网络的基础适配器
- 打开基础适配器
- 虚拟微型端口 WDK 网络
- 初始化虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e964df868337f520cd460caf90b5648c55b440
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324930"
---
# <a name="initializing-virtual-miniports"></a>初始化虚拟微型端口





中间的驱动程序初始化其虚拟微型端口之后它已成功打开基础的微型端口适配器和已准备好接受请求，但在其虚拟微型端口发送。 中间的驱动程序调用[ **NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)从其[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)一个或多个函数若要请求的一个或多个虚拟微型端口初始化的时间。

**请注意**  中间驱动程序不需要调用**NdisIMInitializeDeviceInstanceEx**打开基础的微型端口适配器。 那里没有为虚拟微型端口和打开适配器之间的一对一关系。

 

设置*DriverInstance*的参数**NdisIMInitializeDeviceInstanceEx**为正在初始化虚拟微型端口的设备名称。 中间驱动程序将获取设备名称从**UpperBindings**注册表项。

有关*n*-到-一个 MUX 中间层通过单个物理 NIC 的多个虚拟微型端口驱动程序，但必须在每个虚拟微型端口的设备名称。 MUX 中间驱动程序需要维护虚拟微型端口设备名称的列表的通知对象。 建议在此位置的列表是**UpperBindings**注册表项。 在这种情况下， **UpperBindings**注册表项是一个多\_SZ 条目包含设备名称的列表。 MUX 中间驱动程序调用**NdisIMInitializeDeviceInstanceEx**一次针对设备名称列表中指定每个设备名称。

调用**NdisIMInitializeDeviceInstanceEx**中间驱动程序的调用会导致[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数来执行的初始化指定虚拟微型端口，前提是 NDIS 接收 IRP\_MN\_启动\_设备以启动设备。 如果 NDIS 不会接收此类 IRP，NDIS 将不会调用中间驱动程序*MiniportInitializeEx*函数。 在调用*MiniportInitializeEx*在更高版本时可能发生，因此不一定是对的调用的上下文中**NdisIMInitializeDeviceInstanceEx**。 如果从未调用 NDIS *MiniportInitializeEx*的调用中引用虚拟微型端口**NdisIMInitializeDeviceInstanceEx**，且中间驱动程序不再需要虚拟微型端口，中间驱动程序应调用[ **NdisIMCancelInitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562719)取消初始化虚拟微型端口。 例如，假设中间的驱动程序创建虚拟微型端口绑定到基础的微型端口的成功响应。 如果在 NDIS 调用之前删除该绑定*MiniportInitializeEx*，中间驱动程序应调用**NdisIMCancelInitializeDeviceInstance**取消的微型端口初始化。

*MiniportInitializeEx*必须分配并初始化虚拟微型端口特定的上下文区域。 有关指定的上下文区域的详细信息，请参阅[初始化虚拟微型端口](initializing-a-virtual-miniport.md)。

中间的驱动程序必须作为反序列化的驱动程序运行。 有关反序列化的驱动程序的详细信息，请参阅[反序列化的 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

中间的驱动程序应该验证正确初始化它所维护的状态信息。 如果驱动程序需要发送相关资源--例如，new [ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)网络数据的结构的[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)会将传输到下一个较低层-NET\_缓冲区\_列表结构池可以分配这一次。

 

 





