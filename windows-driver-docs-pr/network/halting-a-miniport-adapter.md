---
title: 停止微型端口适配器
description: 停止微型端口适配器
ms.assetid: fd57a2b1-593d-412b-96b5-eabd3ea392e0
keywords:
- 正在停止的微型端口适配器 WDK 网络
- 适配器 WDK 网络，正在停止
- 非暂停的状态下 WDK 网络
- MiniportHaltEx
- 正在停止适配器
- 正在停止适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f267239759d55483fb078efab3ff264501468b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565910"
---
# <a name="halting-a-miniport-adapter"></a>停止微型端口适配器





NDIS 调用 NDIS 微型端口驱动程序的[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数从系统中删除适配器时释放资源并停止硬件。 可以调用 NDIS *MiniportHaltEx*驱动程序的后[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数将返回成功。 有关详细信息*MiniportInitializeEx*，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)必须释放该驱动程序分配给设备的任何资源。 该驱动程序必须调用的倒数**Ndis * Xxx*** 函数与它最初分配的资源。 作为一般规则*MiniportHaltEx*函数应调用倒数**Ndis * Xxx*** 在初始化期间使用的相反顺序的函数。

如果适配器生成中断，微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数可由驱动程序的抢占[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)函数之前*MiniportHaltEx*禁用中断。

NDIS 不会调用[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388) OID 是否有未完成请求，或将请求发送。 NDIS 将受影响的设备没有进一步请求提交后 NDIS 调用*MiniportHaltEx*。

之后[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)返回时，微型端口驱动程序处于暂停状态。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序终止处理程序](halt-handler.md)

[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

 

 






