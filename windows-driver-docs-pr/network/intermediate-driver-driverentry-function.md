---
title: DriverEntry 中间驱动程序函数
description: DriverEntry 中间驱动程序函数
ms.assetid: 85b4d5c0-8ec9-41a9-a34e-578a85d411e3
keywords:
- 中间驱动程序 WDK 网络入口点
- NDIS 中间驱动程序 WDK，入口点
- WDK 网络的入口点
- DriverEntry WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4073c7d612756bdbd4535979deb59795089dfced
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542019"
---
# <a name="intermediate-driver-driverentry-function"></a>DriverEntry 中间驱动程序函数





必须显式命名为中间驱动程序的初始所需的入口点[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) ，以便加载程序可以正确标识它。 所有其他导出驱动程序函数，为此部分所述*MiniportXxx*并*ProtocolXxx*，可以有供应商指定的任何名称，因为作为地址到 NDIS 传递。

在中间的驱动程序， **DriverEntry**至少必须：

1.  调用[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)并保存中返回的句柄*NdisMiniportDriverHandle*参数。

2.  调用[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)若要注册的驱动程序*ProtocolXxx*函数如果驱动程序随后将本身绑定到基础的 NDIS 驱动程序。

3.  调用[ **NdisIMAssociateMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff562717)通知 NDIS 驱动程序的微型端口上边缘与协议下边缘之间的关联。

中间的驱动程序必须注册[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)卸载处理程序。 在系统中卸载中间驱动程序时，将调用此卸载处理程序。 如果[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)失败，不调用此卸载处理程序; 而是只需卸载该驱动程序。 有关卸载处理程序的详细信息，请参阅[卸载 Intermediate Driver](unloading-an-intermediate-driver.md)。

卸载处理程序应调用[ **NdisDeregisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff561743)能够取消注册中间驱动程序的协议部分。 卸载处理程序还应执行任何必要的清理操作，例如重新分配使用该驱动程序的协议一部分的资源。

请注意，卸载处理程序不同于[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数： 卸载处理程序具有更多全局作用域和范围*MiniportHaltEx*函数限制为特定的微型端口适配器。 中间的驱动程序应清理状态信息和每个绑定到它的基础的微型端口驱动程序将停止时重新分配资源。 有关处理虚拟微型端口停止操作的信息，请参阅[停止虚拟微型端口](halting-a-virtual-miniport.md)。

[*ProtocolUninstall* ](https://msdn.microsoft.com/library/windows/hardware/ff570279)是一个可选的卸载处理程序。 注册中此函数的入口点*ProtocolCharacteristics*结构，它将传递给[ **NdisRegisterProtocolDriver**](https://msdn.microsoft.com/library/windows/hardware/ff564520)。 NDIS 调用*ProtocolUninstall*卸载中间驱动程序的用户请求的响应中。 NDIS 调用[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)一次针对每个绑定的适配器，然后调用 NDIS *ProtocolUninstall*。 系统实际上卸载该驱动程序之前调用此处理程序。 提供一个机会发布设备的任何对象或其他资源，否则可能会阻止系统调用注册的卸载处理程序，此计时**NdisMRegisterMiniportDriver**和卸载该驱动程序。

**DriverEntry**可以初始化自旋锁来保护中间驱动程序分配，如状态变量、 结构和内存区域的所有全局共享的资源。 这些资源来跟踪连接并跟踪正在进行或驱动程序分配的队列发送该驱动程序使用。

如果**DriverEntry**无法分配驱动程序所需执行任何资源的网络 I/O 操作，它应释放以前分配的资源，并返回相应的错误状态。

进一步的以下主题介绍如何注册中间驱动程序：

[注册为 NDIS 中间驱动程序](registering-as-an-ndis-intermediate-driver.md)

[注册为微型端口驱动程序的中间驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)

[注册为协议驱动程序的中间驱动程序](registering-an-intermediate-driver-as-a-protocol.md)

 

 





