---
title: 维护网络接口堆栈
description: 维护网络接口堆栈
ms.assetid: c51a2e5b-28ad-4e86-8b37-1491f85a17bb
keywords:
- NDIS 网络接口 WDK，堆栈维护
- 网络接口 WDK，堆栈维护
- 堆栈 WDK 网络
- 接口 stack 表 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 073cd0d20a2343dd8b45d1835dc42984bd9859ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563719"
---
# <a name="maintaining-a-network-interface-stack"></a>维护网络接口堆栈





NDIS 提供服务，来保持接口堆栈表 (*ifStackTable*在 RFC 2863)。 NDIS 维护 NDIS 微型端口适配器，NDIS 5 堆栈表。*x*筛选中间驱动程序和 NDIS 筛选器模块。 NDIS 还提供了服务可用于添加和删除此表中的条目的 NDIS 驱动程序。 MUX 中间驱动程序，请 NDIS 没有访问虚拟微型端口接口和协议低接口之间的关系。 因此，NDIS 6.0 MUX 中间驱动程序必须指定这些内部接口关系。

若要定义两个接口之间的堆栈关系，任何 NDIS 驱动程序可以将传递*HigherLayerIfIndex*并*LowerLayerIfIndex*参数[ **NdisIfAddIfStackEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff562693)函数。 这些参数指定应为更高版本中的网络接口堆栈和应该在堆栈中较低的一个网络接口的一个网络接口。

有关与另一个接口 （例如，内部绑定 MUX 中间驱动程序中看不到 NDIS） 相关的接口具有堆栈订单信息的驱动程序调用**NdisIfAddIfStackEntry**来填充接口堆栈表。 此函数将返回 NDIS\_状态\_如果已成功进行的堆栈项是成功。 通常情况下，拥有或更高的层接口的接口提供程序的组件 (其中*HigherLayerIfIndex*标识) 调用**NdisIfAddIfStackEntry**。

若要删除堆栈表条目，驱动程序将传递*HigherLayerIfIndex*并*LowerLayerIfIndex*参数[ **NdisIfDeleteIfStackEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff562698)函数。

有关维护界面栈的示例，请参阅 MUX 6.0 示例驱动程序。

 

 





