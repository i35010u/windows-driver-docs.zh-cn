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
ms.openlocfilehash: 6e808d8171210c2b1fc70a4f7cd27f308a169a7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568720"
---
# <a name="halting-a-virtual-miniport"></a>停止虚拟微型端口





如果 NDIS 中间层驱动程序调用[ **NdisIMDeinitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562721)函数、 NDIS 调用[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)受影响的虚拟微型端口函数。 中间的驱动程序通常调用**NdisIMDeInitializeDeviceInstance**从其[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数。

NDIS 集*HaltAction*参数**NdisHaltDeviceInstanceDeInitialized**指示 NDIS 导致停止响应中间驱动程序的调用中的适配器**NdisIMDeInitializeDeviceInstance**函数。

在中间驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数必须释放与虚拟微型端口相关联的所有驱动程序分配资源。

 

 





