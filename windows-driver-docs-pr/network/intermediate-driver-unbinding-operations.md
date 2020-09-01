---
title: 中间驱动程序取消绑定操作
description: 中间驱动程序取消绑定操作
ms.assetid: d316385a-9481-4708-9e09-06d0424acd8f
keywords:
- 中间驱动程序 WDK 网络，绑定
- NDIS 中间驱动程序 WDK，绑定
- 取消绑定 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2161e2360ad51ee45aeb79526ffcaaab058da949
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212901"
---
# <a name="intermediate-driver-unbinding-operations"></a>中间驱动程序取消绑定操作





中间驱动程序通过从基础微型端口驱动程序调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) ，从其 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数中解除绑定。 如果基础微型端口适配器不再可用，NDIS 将调用 *ProtocolUnbindAdapterEx* 。

当驱动程序具有对[**NdisIMInitializeDeviceInstanceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)的未处理调用时，可以调用中间驱动程序的*ProtocolUnbindAdapterEx*函数。 当 NDIS 尚未调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 初始化相应的虚拟微型端口时，会发生这种情况。 在这种情况下，中间驱动程序必须调用 [**NdisIMCancelInitializeDeviceInstance**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimcancelinitializedeviceinstance) 来尝试取消初始化这些虚拟微型端口。

如果正在关闭的绑定映射到由中间驱动程序导出的设备，并且该设备已通过调用 [**NdisIMInitializeDeviceInstanceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)初始化，则中间驱动程序可以调用 [**NdisIMDeInitializeDeviceInstance**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance) 来关闭该设备。 结果是，中间驱动程序的虚拟小型端口将不再可用于更高级别驱动程序发出或发出的请求。

如果 NDIS 中间驱动程序调用 **NdisIMDeInitializeDeviceInstance** 函数，ndis 将为受影响的虚拟小型端口调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 有关处理虚拟微型端口的暂停操作的信息，请参阅 [停止虚拟微型端口](halting-a-virtual-miniport.md)。

中间驱动程序调用 **NdisCloseAdapterEx**后，该绑定的任何发送请求都将失败，并出现相应的错误状态。

有关中间驱动程序取消绑定操作的其他信息，请参阅 [从适配器解除绑定](unbinding-from-an-adapter.md)。

 

