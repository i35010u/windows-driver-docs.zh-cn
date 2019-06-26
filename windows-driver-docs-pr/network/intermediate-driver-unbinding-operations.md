---
title: 中间驱动程序取消绑定操作
description: 中间驱动程序取消绑定操作
ms.assetid: d316385a-9481-4708-9e09-06d0424acd8f
keywords:
- 中间驱动程序 WDK 网络、 绑定
- NDIS 中间驱动程序 WDK、 绑定
- 正在取消绑定 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e748cebdc37b238cb2997a6125db9cee2e1bf1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354550"
---
# <a name="intermediate-driver-unbinding-operations"></a>中间驱动程序取消绑定操作





取消绑定从基础的微型端口驱动程序的中间驱动程序通过调用[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)从其[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。 NDIS 调用*ProtocolUnbindAdapterEx*如果基础的微型端口适配器不再可用。

中间驱动程序的*ProtocolUnbindAdapterEx*驱动程序必须对的未完成调用时，可能调用函数[ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)。 NDIS 尚未调用时发生这种情况下[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)初始化相应的虚拟微型端口。 在这种情况下，中间驱动程序必须调用[ **NdisIMCancelInitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimcancelinitializedeviceinstance)尝试取消这些虚拟微型端口的初始化。

如果正在关闭的绑定将映射到由中间驱动程序导出的设备，并且该设备已通过调用来初始化[ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)，中间驱动程序可以调用[ **NdisIMDeInitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)关闭设备。 结果是中间驱动程序的虚拟微型端口变得不再可用于发送或由更高级别的驱动程序发出的请求。

如果 NDIS 中间层驱动程序调用**NdisIMDeInitializeDeviceInstance**函数，将调用 NDIS [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数为受影响的虚拟微型端口. 有关处理虚拟微型端口停止操作的信息，请参阅[停止虚拟微型端口](halting-a-virtual-miniport.md)。

中间的驱动程序调用后**NdisCloseAdapterEx**，这应该会失败的相应的错误状态将显示与该绑定的任何发送请求。

有关中间驱动程序正在取消绑定操作的其他信息，请参阅[取消绑定从适配器](unbinding-from-an-adapter.md)。

 

 





