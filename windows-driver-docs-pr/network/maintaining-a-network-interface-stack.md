---
title: 维护网络接口堆栈
description: 维护网络接口堆栈
ms.assetid: c51a2e5b-28ad-4e86-8b37-1491f85a17bb
keywords:
- NDIS 网络接口 WDK，堆栈维护
- 网络接口 WDK，堆栈维护
- 堆栈 WDK 网络
- 接口堆栈表 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc8954262f47fb7242b76cc1c8220b103220484
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844134"
---
# <a name="maintaining-a-network-interface-stack"></a>维护网络接口堆栈





NDIS 提供服务来维护接口堆栈表（RFC 2863 中的*ifStackTable* ）。 NDIS 维护 NDIS 端口适配器的堆栈表，NDIS 5。*x*筛选器中间驱动程序和 NDIS 筛选器模块。 NDIS 还提供服务，使 NDIS 驱动程序能够在此表中添加和删除条目。 对于 MUX 中间驱动程序，NDIS 无法访问虚拟微型端口接口和协议下限接口之间的关系。 因此，NDIS 6.0 MUX 中间驱动程序必须指定这些内部接口关系。

若要在两个接口之间定义堆栈关系，任何 NDIS 驱动程序都可以将*HigherLayerIfIndex*和*LowerLayerIfIndex*参数传递到[**NdisIfAddIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry)函数。 这些参数指定一个网络接口，该接口应位于网络接口堆栈中的更高位置，以及一个应在堆栈中较低的网络接口。

一个驱动程序，该驱动程序具有有关与其他接口相关的接口的堆栈顺序信息（例如，在 MUX 中间驱动程序中不可见的内部绑定）调用**NdisIfAddIfStackEntry**来填充接口堆栈表. 如果成功创建了堆栈条目，则此函数将返回 NDIS\_状态\_成功。 通常，拥有或是更高层接口（ *HigherLayerIfIndex*标识）的接口提供程序的组件调用**NdisIfAddIfStackEntry**。

若要删除堆栈表项，驱动程序会将*HigherLayerIfIndex*和*LowerLayerIfIndex*参数传递到[**NdisIfDeleteIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifdeleteifstackentry)函数。

有关维护接口堆栈的示例，请参阅 MUX 6.0 示例驱动程序。

 

 





