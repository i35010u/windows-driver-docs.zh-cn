---
title: 分配接口索引
description: 分配接口索引
keywords:
- NDIS 网络接口 WDK，接口索引分配
- 网络接口 WDK，接口索引分配
- 接口索引 WDK 网络
- 正在分配网络接口索引
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f066ec562e09e5f3cc75bc78b25c333c5539dc4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825551"
---
# <a name="allocating-an-interface-index"></a>分配接口索引





如果接口提供程序通过调用 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数成功注册接口，NDIS 将为该接口分配一个接口索引，并返回 *pIfIndex* 参数指定的位置处的索引值。 接口索引是在本地计算机上唯一的16位值。 在计算机重新启动后，如果接口提供程序注册了相同的 [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 值，NDIS 不保证它将分配相同的接口索引。 接口索引值 0 (NET \_ IFINDEX \_ 未指定) 保留，并且 NDIS 不会将其分配给任何接口。

 

