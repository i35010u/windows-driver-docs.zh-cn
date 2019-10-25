---
title: 停止虚拟微型端口
description: 停止虚拟微型端口
ms.assetid: f53040b1-cbbc-4b13-9bc7-8fae9eb38391
keywords:
- 停止虚拟微型端口
- virtual 微型端口 WDK 网络
- NDIS 中间驱动程序 WDK，virtual 微型端口
- 中间驱动程序 WDK 网络，虚拟微型端口
- 正在停止虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bb4dcaf9641ba7ad130037e0a489bf54da81f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842118"
---
# <a name="halting-a-virtual-miniport"></a>停止虚拟微型端口





如果 NDIS 中间驱动程序调用[**NdisIMDeinitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance)函数，ndis 将为受影响的虚拟小型端口调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。 中间驱动程序通常从其[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数调用**NdisIMDeInitializeDeviceInstance** 。

NDIS 将*HaltAction*参数设置为**NdisHaltDeviceInstanceDeInitialized** ，以指示 NDIS 正在停止适配器，以响应对**NdisIMDeInitializeDeviceInstance**函数的中间驱动程序调用。

中间驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数必须释放与虚拟小型端口关联的所有驱动程序分配的资源。

 

 





