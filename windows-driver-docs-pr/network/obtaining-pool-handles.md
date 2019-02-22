---
title: 获取池处理
description: 获取池处理
ms.assetid: 752b0d64-2ca3-4dc0-a6cd-642e96af1f8f
keywords:
- 池处理 WDK 网络
- 协议驱动程序 WDK 网络，池句柄
- NDIS 协议驱动程序 WDK，池句柄
- 微型端口驱动程序 WDK 网络，池句柄
- NDIS 微型端口驱动程序 WDK，池句柄
- 中间驱动程序 WDK 网络、 采购订单
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ec469bd5831a1901880dc2db55483d0362284a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544512"
---
# <a name="obtaining-pool-handles"></a>获取池处理





以下 NDIS 池分配函数需要分配资源的句柄：

-   [**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)

-   [**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)

NDIS 6.0 驱动程序，如下所示获取句柄：

<a href="" id="protocol-drivers"></a>协议驱动程序  
协议驱动程序调用[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数来获取句柄。

<a href="" id="miniport-drivers"></a>微型端口驱动程序  
NDIS 调用[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数以将该句柄传递给微型端口驱动程序。

<a href="" id="intermediate-drivers"></a>中间驱动程序  
驱动程序调用的中间[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数中使用的池发送操作和 NDIS 获取句柄调用*MiniportInitializeEx*到将句柄传递给中间驱动程序，用于在中使用的池接收操作。

<a href="" id="filter-drivers"></a>筛选器驱动程序  
NDIS 调用[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数以将该句柄传递给筛选器驱动程序。

<a href="" id="other-drivers"></a>其他驱动程序  
如果驱动程序无法通过上述方法之一获取句柄，该驱动程序可以调用[ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)函数来获取的句柄。

 

 





