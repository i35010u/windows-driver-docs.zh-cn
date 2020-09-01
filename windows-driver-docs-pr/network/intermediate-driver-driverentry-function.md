---
title: 中间驱动程序 DriverEntry 函数
description: 中间驱动程序 DriverEntry 函数
ms.assetid: 85b4d5c0-8ec9-41a9-a34e-578a85d411e3
keywords:
- 中间驱动程序 WDK 网络，入口点
- NDIS 中间驱动程序 WDK，入口点
- 入口点 WDK 网络
- DriverEntry WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ecdf914b4d66b64b4fc383c5133000ece618b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215628"
---
# <a name="intermediate-driver-driverentry-function"></a>中间驱动程序 DriverEntry 函数





中间驱动程序的初始必需入口点必须显式命名为 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) ，以便加载程序能够正确地识别它。 本部分中描述的所有其他已导出驱动程序函数（如 *MiniportXxx* 和 *ProtocolXxx*）可以具有任何供应商指定的名称，因为它们将作为地址传递到 NDIS。

在中间驱动程序中， **DriverEntry** 必须至少：

1.  调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 并保存 *NdisMiniportDriverHandle* 参数中返回的句柄。

2.  如果驱动程序随后将自身绑定到基础 NDIS 驱动程序，请调用 [**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 来注册驱动程序的 *ProtocolXxx* 函数。

3.  调用 [**NdisIMAssociateMiniport**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimassociateminiport) ，告知 NDIS 有关驱动程序的小型端口上边缘与协议下限之间的关联的信息。

中间驱动程序必须注册 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload) 卸载处理程序。 当系统卸载中间驱动程序时，将调用此卸载处理程序。 如果 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 失败，则不会调用此卸载处理程序;相反，驱动程序只是卸载。 有关卸载处理程序的详细信息，请参阅 [卸载中间驱动程序](unloading-an-intermediate-driver.md)。

卸载处理程序应调用 [**NdisDeregisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver) 来取消注册中间驱动程序的协议部分。 卸载处理程序还应执行任何必要的清理操作，如重新分配驱动程序的协议部分所使用的资源。

请注意，卸载处理程序与 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数不同：卸载处理程序具有更全局的作用域， *MiniportHaltEx* 函数的作用域限制为特定的微型端口适配器。 中间驱动程序应清除状态信息，并在每个绑定到它的基础微型端口驱动程序停止时重新分配资源。 有关处理虚拟微型端口的暂停操作的信息，请参阅 [停止虚拟微型端口](halting-a-virtual-miniport.md)。

[*ProtocolUninstall*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall) 是一个可选的卸载处理程序。 在传递到[**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)的*ProtocolCharacteristics*结构中注册此函数的入口点。 为了响应用户请求以卸载中间驱动程序，NDIS 调用了 *ProtocolUninstall* 。 对于每个绑定适配器，NDIS 都调用一次 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) ，并调用 *ProtocolUninstall*。 在系统实际卸载驱动程序之前，将调用此处理程序。 这种计时使你可以释放任何设备对象或其他资源，否则可能会阻止系统调用已注册到 **NdisMRegisterMiniportDriver** 并卸载驱动程序的卸载处理程序。

**DriverEntry** 可以初始化自旋锁，以保护中间驱动程序分配的任何全局共享资源，如状态变量、结构和内存区域。 驱动程序使用这些资源跟踪连接并跟踪正在进行的发送或驱动程序分配的队列。

如果 **DriverEntry** 无法分配驱动程序执行网络 i/o 操作所需的任何资源，则它应释放以前分配的任何资源并返回相应的错误状态。

以下主题进一步说明了如何注册中间驱动程序：

[注册为 NDIS 中间驱动程序](registering-as-an-ndis-intermediate-driver.md)

[将中间驱动程序注册为微型端口驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)

[将中间驱动程序注册为协议驱动程序](registering-an-intermediate-driver-as-a-protocol.md)

 

