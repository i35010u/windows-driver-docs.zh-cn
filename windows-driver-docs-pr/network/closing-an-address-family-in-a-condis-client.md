---
title: 关闭的 CoNDIS 客户端中的地址族
description: 关闭的 CoNDIS 客户端中的地址族
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- 客户端关闭 AFs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1ca0437d033078b39fcdec57387f4774fe7f549
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534276"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>关闭的 CoNDIS 客户端中的地址族





若要关闭 AFs，CoNDIS 客户端必须提供[ **ProtocolClNotifyCloseAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570234)函数。 NDIS 调用*ProtocolClNotifyCloseAf*当独立呼叫管理器或 MCM 调用[ **NdisCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561680)函数或[ **NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546)函数，分别。

从内部*ProtocolClNotifyCloseAf*、 在客户端完成关闭指定的 AF，或返回 NDIS\_状态\_PENDING 和调用[ **NdisClNotifyCloseAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561638)函数来完成该操作。 客户端调用后**NdisClNotifyCloseAddressFamilyComplete**，NDIS 调用[ **ProtocolCmNotifyCloseAfComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570248)函数，以通知呼叫管理器，客户端关闭 AF。

若要关闭 AF，客户端应：

1.  如果客户端有活动的多点连接，调用[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)函数根据需要多次，直到一个参与方将保持活动状态在每个 multipoint 虚拟连接 (VC)。

2.  调用[ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)函数，根据需要关闭的所有调用的仍是打开的都与的地址族。

3.  调用[ **NdisClDeregisterSap** ](https://msdn.microsoft.com/library/windows/hardware/ff561628)函数根据需要取消注册的所有服务访问点 (SAPs) 与呼叫管理器注册了客户端的次数。

4.  调用[ **NdisClCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561626)函数以关闭 AF。

 

 





