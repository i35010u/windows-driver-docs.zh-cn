---
title: 停止虚拟微型端口
description: 停止虚拟微型端口
ms.assetid: f53040b1-cbbc-4b13-9bc7-8fae9eb38391
keywords:
- 正在停止虚拟微型端口
- 虚拟微型端口 WDK 网络
- NDIS 中间层驱动程序 WDK，虚拟微型端口
- 中间驱动程序 WDK 网络、 虚拟微型端口
- 正在停止虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57852bcba2ea4b12d703303b9ebe6dd3937be2aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379831"
---
# <a name="halting-a-virtual-miniport"></a>停止虚拟微型端口





如果 NDIS 中间层驱动程序调用[ **NdisIMDeinitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)函数、 NDIS 调用[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)受影响的虚拟微型端口函数。 中间的驱动程序通常调用**NdisIMDeInitializeDeviceInstance**从其[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

NDIS 集*HaltAction*参数**NdisHaltDeviceInstanceDeInitialized**指示 NDIS 导致停止响应中间驱动程序的调用中的适配器**NdisIMDeInitializeDeviceInstance**函数。

在中间驱动程序[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数必须释放与虚拟微型端口相关联的所有驱动程序分配资源。

 

 





