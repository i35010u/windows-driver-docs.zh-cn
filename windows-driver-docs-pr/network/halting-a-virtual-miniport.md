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
ms.openlocfilehash: 3a0d5b8d85a4f33895f6fcf1b5ae71c6d81a8c83
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211772"
---
# <a name="halting-a-virtual-miniport"></a>停止虚拟微型端口





如果 NDIS 中间驱动程序调用 [**NdisIMDeinitializeDeviceInstance**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance) 函数，ndis 将为受影响的虚拟小型端口调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 中间驱动程序通常从其[*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数调用**NdisIMDeInitializeDeviceInstance** 。

NDIS 将 *HaltAction* 参数设置为 **NdisHaltDeviceInstanceDeInitialized** ，以指示 NDIS 正在停止适配器，以响应对 **NdisIMDeInitializeDeviceInstance** 函数的中间驱动程序调用。

中间驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数必须释放与虚拟小型端口关联的所有驱动程序分配的资源。

 

