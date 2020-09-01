---
title: 初始化虚拟微型端口
description: 初始化虚拟微型端口
ms.assetid: b712fe29-fd56-4abd-bab6-e335350a20c2
keywords:
- 打开 WDK 网络的基础适配器
- 打开基础适配器
- virtual 微型端口 WDK 网络
- 正在初始化虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3559f7083212e9d3d9f75e47f62e918397e9374
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218408"
---
# <a name="initializing-virtual-miniports"></a>初始化虚拟微型端口





中间驱动程序在成功打开基础微型端口适配器后初始化其虚拟微型端口，并已准备好接受请求并在其虚拟微型端口上发送。 中间驱动程序一次或多次调用 [**NdisIMInitializeDeviceInstanceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex) 的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数，请求初始化一个或多个虚拟微型端口。

**注意**   中间驱动程序在打开基础微型端口适配器时，不需要调用**NdisIMInitializeDeviceInstanceEx** 。 虚拟微型端口和开放式适配器之间不一定存在一对一关系。

 

将**NdisIMInitializeDeviceInstanceEx**的*DriverInstance*参数设置为要初始化的虚拟微型端口的设备名称。 中间驱动程序从 **UpperBindings** 注册表项中获取设备名称。

对于在单个物理 NIC 上对多个虚拟微型端口进行分层的 *n*对一 MUX 中间驱动程序，每个虚拟小型端口必须有一个设备名称。 MUX 中间驱动程序需要一个通知对象，该对象维护虚拟微型端口设备名称的列表。 建议的列表位置是 **UpperBindings** 注册表项。 在这种情况下， **UpperBindings** 注册表项是 \_ 包含设备名称列表的多 SZ 项。 MUX 中间驱动程序对 "设备名称" 列表中指定的每个设备名称调用 **NdisIMInitializeDeviceInstanceEx** 一次。

调用 **NdisIMInitializeDeviceInstanceEx** 会导致调用中间驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数来执行指定虚拟小型端口的初始化，前提是 NDIS 接收 IRP \_ MN \_ 启动 \_ 设备以启动设备。 如果 NDIS 未收到这样的 IRP，NDIS 将不会调用中间驱动程序的 *MiniportInitializeEx* 函数。 对 *MiniportInitializeEx* 的调用可能会在稍后发生，因此不一定会出现在对 **NdisIMInitializeDeviceInstanceEx**的调用的上下文中。 如果 NDIS 绝不会调用对**NdisIMInitializeDeviceInstanceEx**的调用中引用的虚拟微型端口的*MiniportInitializeEx* ，而中间驱动程序不再需要虚拟小型端口，中间驱动程序应调用[**NdisIMCancelInitializeDeviceInstance**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimcancelinitializedeviceinstance)来取消虚拟小型端口的初始化。 例如，假设中间驱动程序创建虚拟小型端口，以响应到基础微型端口的成功绑定。 如果在 NDIS 调用 *MiniportInitializeEx*之前删除该绑定，中间驱动程序应调用 **NdisIMCancelInitializeDeviceInstance** 来取消小型端口的初始化。

*MiniportInitializeEx* 必须分配和初始化虚拟微型端口专用的上下文区域。 有关指定上下文区域的详细信息，请参阅 [初始化虚拟微型端口](initializing-a-virtual-miniport.md)。

中间驱动程序必须作为反序列化的驱动程序运行。 有关反序列化驱动程序的详细信息，请参阅 [反序列化 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

中间驱动程序应该验证其维护的状态信息是否已正确初始化。 如果驱动程序需要与发送相关的资源（例如， [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)将传输到下一个较低层的网络数据的新网络[** \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构），则 \_ \_ 此时可以分配网络缓冲区列表结构池。

 

